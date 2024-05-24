# Lines of code

https://github.com/pixeldaogg/florida-contracts/blob/10d48b51313496c41c886cd46e610b627ef159aa/src/lib/AuctionLoanLiquidator.sol#L283


# Vulnerability details

## Impact

There is a race condition between the `placeBid()` and `settleAuction()` functions when `block.timestamp == maxExtension`.

```solidity

// @audit check in `placeBid()`
/// @dev max (min(withMargin, maxExtension), expiration)
uint96 max = minWithMarginMaxExtension > expiration ? minWithMarginMaxExtension : expiration;
if (max < currentTime && currentHighestBid != 0) {
  revert AuctionOverError(max);
}

// @audit check in `settleAuction()`
if ((withMargin > currentTime && currentTime < maxExtension) || (currentTime < expiration)) {
    ...
    revert AuctionNotOverError(max);
}
```

As seen in the code snippet, the `placeBid()` function will revert if `currentTime > maxExtension` while the `settleAuction()` function will revert if `currentTime < maxExtension`.

This implies that both functions can be used when `currentTime == maxExtension`.

## Recommended Mitigation Steps
Only allowing to call `settleAuction()` when `currentTime > maxExtension`.



## Assessed type

Timing