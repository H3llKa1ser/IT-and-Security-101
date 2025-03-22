# Microsoft Defender for Cloud Secure Score

Microsoft Defender for Cloud has two main goals:

1) To help you understand your current security situation

2) To help you efficiently and effectively improve your security

The central feature in Defender for Cloud that enables you to achieve those goals is the secure score.

Defender for Cloud continually assesses your cross-cloud resources for security issues. It then aggregates all the findings into a single score so that you can tell, at a glance, your current security situation: the higher the score, the lower the identified risk level.

To increase your security, review Defender for Cloud's recommendations page and remediate the recommendation by implementing the remediation instructions for each issue. Recommendations are grouped into security controls. Each control is a logical group of related security recommendations and reflects your vulnerable attack surfaces. Your score only improves when you remediate all of the recommendations for a single resource within a control. To see how well your organization is securing each individual attack surface, review the scores for each security control.

## How your secure score is calculated

To get all the possible points for security control, all of your resources must comply with all of the security recommendations within the security control. For example, Defender for Cloud has multiple recommendations regarding how to secure your management ports. You'll need to remediate them all to make a difference to your secure score.

## Which recommendations are included in the secure score calculations?

Only built-in recommendations have an impact on the secure score.

Recommendations flagged as Preview aren't included in the calculations of your secure score. They should still be remediated wherever possible so that when the preview period ends, they'll contribute towards your score.

Preview recommendations are marked with:

![image](https://github.com/user-attachments/assets/2663edbc-c7f2-468f-bd51-0bfe462bdfe0)

## Improve your secure score

To improve your secure score, remediate security recommendations from your recommendations list. You can remediate each recommendation manually for each resource or use the Fix option (when available) to resolve an issue on multiple resources quickly.

You can also configure the Enforce and Deny options on the relevant recommendations to improve your score and make sure your users don't create resources that negatively impact your score.

