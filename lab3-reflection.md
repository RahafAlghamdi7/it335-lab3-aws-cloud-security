# Lab 3 Reflection – AWS Cloud Security Fundamentals (Capital One Case Study)

## Summary of Configurations

In this lab, I configured foundational AWS security controls across four key areas: Identity and Access Management (IAM), secure storage using S3, secured compute through EC2, and visibility through logging and billing tools.

For IAM, I reviewed the root account security and confirmed that Multi-Factor Authentication (MFA) was not enabled, which represents a potential security risk. I then created a restricted IAM group called "LabUsers" with ReadOnlyAccess permissions and added a new IAM user to that group. This demonstrated the principle of least privilege by avoiding the use of the root account for daily tasks.

For S3, I created a new bucket and ensured that "Block all public access" was enabled. This configuration prevents the bucket from being publicly accessible and protects any stored data from unauthorized access.

For EC2, I launched a Free Tier instance and configured its security group to allow SSH access only from my own IP address. This avoided exposing the instance to the public internet (0.0.0.0/0), significantly reducing the attack surface. I also reviewed instance metadata settings and noted the importance of secure configurations such as IMDSv2.

For visibility and governance, I accessed the Billing dashboard and CloudTrail service. Billing provides cost monitoring, while CloudTrail logs API activity across the AWS environment, both of which are critical for detecting suspicious behavior.

---

## Connection to the Capital One Breach

Each configuration directly addresses key failures observed in the Capital One incident.

The use of least-privilege IAM controls limits the impact of compromised credentials. In the Capital One breach, overly permissive IAM roles allowed the attacker to access sensitive data. By restricting permissions, the potential damage from stolen credentials is significantly reduced.

The S3 "Block all public access" setting directly prevents accidental exposure of sensitive data. In the Capital One case, misconfigured storage contributed to data exfiltration. Ensuring that buckets are private by default is a critical defense.

The EC2 configuration, particularly restricting security group access and considering IMDSv2, helps prevent exploitation paths such as Server-Side Request Forgery (SSRF). In the breach, SSRF was used to access instance metadata and obtain credentials. Limiting network access and securing metadata services disrupts this attack chain.

Finally, CloudTrail and billing awareness improve detection capabilities. In the Capital One incident, insufficient monitoring allowed the attacker to remain undetected for an extended period. Continuous logging and monitoring reduce this window of opportunity by enabling faster identification of suspicious activity.

---

## Critical Analysis

The IAM and S3 configurations were relatively straightforward to implement and provided immediate security benefits. In contrast, security groups in EC2 require careful attention, as it is easy to accidentally allow overly broad access such as 0.0.0.0/0, which can introduce significant risk.

This lab also highlighted that security tools alone are not sufficient. Organizational culture and governance play a critical role in ensuring that best practices are consistently followed. Even with the availability of secure configurations, human error or lack of oversight can lead to misconfigurations, as seen in the Capital One breach. Proper training, policies, and continuous monitoring are essential to maintaining a secure cloud environment.
