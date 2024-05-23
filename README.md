# Gondi Mitigation Review

Competition findings are submitted to this repo.

Unless otherwise discussed, this repo will be made public after competition completion, sponsor review, judging, and issue mitigation window.

**Contributors to this repo:** prior to report publication, please review the [Agreements & Disclosures](../../issues/1) issue.

**Note that when the repo is public, after all issues are mitigated, your comments will be publicly visible; they may also be included in your C4 audit report.**

---

# Review phase

Sponsors have two critical tasks in the mitigation review process: 

1. [Respond to High- and Medium-risk submissions ↓](#1-respond-to-high--and-medium-risk-submissions)
2. [Provide input on reviews of individual mitigations ↓](#2-provide-input-on-reviews-of-individual-mitigations)

<hr>

## 1. Respond to High- and Medium-risk submissions

### [High/Medium-risk findings for review →](../../issues?q=is%3Aopen+is%3Aissue+label%3A"2+%28Med+Risk%29"%2C"3+%28High+Risk%29"+-label%3A"unsatisfactory"%2C"insufficient+quality+report"%2C"sponsor+acknowledged"%2C"sponsor+confirmed"%2C"sponsor+disputed"%2C"unmitigated"%2C"mitigation-confirmed"+)

<sup>This list will shorten as you work. [View the original, longer list →](../../issues?q=is%3Aopen+is%3Aissue+label%3A"2+%28Med+Risk%29"%2C"3+%28High+Risk%29"+-label%3A"unsatisfactory"%2C"insufficient+quality+report"%2C"unmitigated"%2C"mitigation-confirmed"+)</sup>

The participating wardens searched for any new High- or Medium-risk vulnerabilities that may have been missed during the preceding C4 audit or introduced via code changes.

For each High- or Medium-risk finding, please:

### 1a. Label as one of the following:

- `sponsor confirmed`, meaning: "Yes, this is a problem and we intend to fix it."
- `sponsor disputed`, meaning either: "We cannot duplicate this issue" or "We disagree that this is an issue at all."
- `sponsor acknowledged`, meaning: "Yes, technically the issue is correct, but we are not going to resolve it for xyz reasons."

Add any necessary comments explaining your rationale for your evaluation of the issue.

Note: Adding or changing labels other than those in this list will be automatically reverted by our bot, which will note the change in a comment on the issue.

### 1b. Weigh in on severity

If you believe a finding is technically correct but disagree with the listed severity, **leave a comment indicating your reasoning** for the judge to review.
For a detailed breakdown of severity criteria and how to estimate risk, please refer to the [judging criteria in our documentation](https://docs.code4rena.com/awarding/judging-criteria/severity-categorization).

Judges have the ultimate discretion in determining validity and severity of issues, as well as whether/how issues are considered duplicates. However, sponsor input is a significant criterion.

<hr>

## 2. Provide input on warden assessments

### [Warden assessments for review →](../../issues?q=is%3Aopen+is%3Aissue+label%3Amitigation-confirmed%2Cunmitigated+-label%3Aunsatisfactory+-label%3A"insufficient+quality+report")

The participating wardens were also tasked with submitting an assessment of the status of every in-scope vulnerability from the original audit. Their reviews should classify each original vulnerability as either `mitigation confirmed` or `unmitigated` alongside their reasoning.

While you're not required to add labels to each of these issues, we invite you to review and comment if you feel there's any additional context that might be helpful for the judge to consider.

## Once Step 1 and 2 are complete

When you have finished labeling and responding to findings, drop the C4 team a note in your private Discord backroom channel and let us know you've completed the sponsor review process. At this point, we will pass the repo over to the judge to review your feedback while you work on mitigations.


<hr>
