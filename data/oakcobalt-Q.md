# Lines of code

https://github.com/pixeldaogg/florida-contracts/blob/7bacbe3f2b4c1bb6c87961e3553118a6e6c2dcee/src/lib/pools/Pool.sol#L423


# Vulnerability details

### Impacts
Auction proceeds might be distributed to an incorrect queue, due to incorrect loan contract used in `_loanTermination()`.

### Proof of concept
Whenever a loan is closed (repaid or liquidation auction settlements) the correct loan contract(MultiSourceLoan address) where the loan is initiated needs to be passed to Pool::_loanTermination to determine the queue where the payment belongs.

In `_loanTermination()`, `getLastLoanId[idx][_loanContract]` will be used to determine the correct queue. 
```solidity
//src/lib/pools/Pool.sol
    function _loanTermination(
|>      address _loanContract,
        uint256 _loanId,
        uint256 _principalAmount,
        uint256 _apr,
        uint256 _interestEarned,
        uint256 _received
    ) private {
...
        for (i = 1; i < totalQueues;) {
            idx = (pendingIndex + i) % totalQueues;
|>          if (getLastLoanId[idx][_loanContract] >= _loanId) {
                break;
            }
```
(https://github.com/pixeldaogg/florida-contracts/blob/7bacbe3f2b4c1bb6c87961e3553118a6e6c2dcee/src/lib/pools/Pool.sol#L556)

The problem is when a loan is terminated in the auction settlement flow. _loanContract can be incorrect. LiquidationDistributor::distribute() will call `LoanManager(_tranche.lender).loanLiquidation()`. And `loanLiquidation()` will pass msg.sender which is LiquidationDistributor address as _loanContract to `_loanTermination()`. 

If LiquidationDistributor is not intended to be a loan contract, `getLastLoanId[idx][_loanContract]` will always return 0. The payment will always go to the pool instead of the correct queue.
```solidity
    function loanLiquidation(
        uint256 _loanId,
        uint256 _principalAmount,
        uint256 _apr,
        uint256,
        uint256 _protocolFee,
        uint256 _received,
        uint256 _startTime
    ) external override {
...
         //@audit msg.sender is LiquidationDistributor, not a loan contract
 |>       _loanTermination(msg.sender, _loanId, _principalAmount, netApr, interestEarned, _received - fees);
```
(https://github.com/pixeldaogg/florida-contracts/blob/7bacbe3f2b4c1bb6c87961e3553118a6e6c2dcee/src/lib/pools/Pool.sol#L423)

### Tools
Manual
### Recommendations
(1) In LiquidationDistributor::distribute() and pool::loanLiquidation() need to pass _auction.loanAddress to be used in _loanTermination(), this will return the correct queue index.
(2) Or always ensure that LiquidationDistributor.sol is added as a loanContract.





## Assessed type

Other