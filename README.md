# AWS S3 Cloud Security Monitoring Project

## Overview
This project demonstrates how common cloud misconfigurations can expose sensitive data in AWS.
The goal was to identify a publicly accessible Amazon S3 bucket, analyze the security risk,
and implement monitoring and remediation using AWS native security services.

---

## Objectives
- Simulate a public S3 bucket misconfiguration
- Detect the exposure using AWS security tools
- Analyze security findings
- Remediate the issue
- Implement continuous monitoring

---

## AWS Services Used
- Amazon S3
- AWS IAM
- AWS CloudTrail
- AWS Config
- Amazon GuardDuty
- Amazon CloudWatch

---

## Lab Environment
- AWS Free Tier account
- Region: us-east-1
- Testing performed only on resources owned by this account

---

## Architecture
User → Public S3 Bucket → CloudTrail Logs → AWS Config Rules → GuardDuty Findings

---

## Security Issue Identified

**Public S3 Bucket Access**

The S3 bucket allowed public read access due to disabled Block Public Access
and an overly permissive bucket policy. This configuration could allow
unauthorized users to access sensitive data.

**Risk Level:** Critical

---

## Detection & Findings

### AWS Config
- Rule: `s3-bucket-public-read-prohibited`
- Status: NON-COMPLIANT
- Finding: Bucket allowed public access

### Amazon GuardDuty
- Detected anomalous access behavior
- Generated security findings related to data exposure

### AWS CloudTrail
- Logged S3 API calls including:
  - GetObject
  - ListBucket
  - PutBucketPolicy

---

## Remediation Steps
- Removed public bucket policy
- Enabled S3 Block Public Access
- Restricted IAM permissions following least privilege
- Verified compliance through AWS Config

---

## Final Result
- S3 bucket is no longer publicly accessible
- AWS Config status changed to COMPLIANT
- Continuous monitoring enabled for future misconfigurations

---

## Key Takeaways
- Public S3 buckets remain one of the most common cloud security risks
- Preventive controls and detective controls must work together
- AWS native security tools provide strong visibility into misconfigurations
- Continuous monitoring is critical in cloud environments

---

## Disclaimer
This project was conducted in a controlled AWS lab environment.
No real user data was used and no production systems were tested.

---

## References
- AWS S3 Security Best Practices  
- NIST SP 800-53  
- MITRE ATT&CK  
