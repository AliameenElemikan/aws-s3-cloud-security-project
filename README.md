# AWS S3 Public Access Incident Detection & Response Lab

## Overview
This project simulates a real-world cloud security incident involving accidental public exposure
of sensitive data stored in Amazon S3. The lab follows a SOC-style workflow to identify,
investigate, and remediate the misconfiguration using AWS-native security services.

The objective was to detect public cloud data exposure, validate findings through security
telemetry, and restore compliance while maintaining audit visibility.

---

## Scenario
During routine cloud monitoring, an Amazon S3 bucket was discovered to be publicly accessible
due to a misconfigured bucket policy and disabled Block Public Access controls.

This condition could allow unauthenticated users on the internet to retrieve stored objects,
resulting in potential data leakage and regulatory exposure.

---

## Skills Demonstrated
- Cloud incident investigation  
- Misconfiguration detection  
- Log-based security monitoring  
- CloudTrail audit analysis  
- AWS Config compliance validation  
- GuardDuty threat monitoring  
- Manual incident remediation  
- Cloud security documentation  

---

## AWS Services Used
- Amazon S3  
- AWS IAM  
- AWS CloudTrail  
- AWS Config  
- Amazon GuardDuty  
- AWS Key Management Service (KMS)  

---

## Lab Environment
- AWS Free Tier account  
- Region: us-east-1  
- Logging encrypted using customer-managed KMS key  
- Testing performed only on resources owned by this account  

---

## Architecture Overview
User → Public S3 Bucket  
↓  
CloudTrail API Logging  
↓  
AWS Config Compliance Rules  
↓  
GuardDuty Threat Detection  
↓  
SOC Investigation & Remediation  

---

# 🔍 Investigation Timeline

---

## Step 1 – S3 Bucket Creation
A test S3 bucket was created to simulate a standard cloud storage resource.

![Bucket Created](01-bucket-created.png)

---

## Step 2 – Sensitive Object Uploaded
A sample file (`customer_data.txt`) was uploaded to represent stored business data.

![File Uploaded](screenshots/02-file-uploaded.png)

---

## Step 3 – Public Access Controls Disabled
Block Public Access was intentionally disabled to simulate a common cloud misconfiguration.

![Block Public Access Off](screenshots/03-block-public-access-off.png)

---

## Step 4 – Public Bucket Policy Applied
A permissive bucket policy was added allowing anonymous read access (`Principal: "*"`) to all objects.

![Public Bucket Policy](screenshots/04-bucket-policy-public.png)

---

## Step 5 – Exposure Confirmation
The object URL was accessed from an unauthenticated browser session, confirming public exposure.

![Public URL Works](screenshots/05-public-url-works.png)

---

# 🔐 Detection & Monitoring

---

## Step 6 – CloudTrail Audit Logging Enabled
CloudTrail was configured to record S3 management and data events, encrypted using KMS.

![CloudTrail Logging](screenshots/06-cloudtrail-trail-created.png)

---

## Step 7 – AWS Config Compliance Rules Enabled
AWS Config rules were deployed to monitor for public S3 access violations.

![Config Rules Enabled](screenshots/07-config-rules-enabled.png)

---

## Step 8 – Compliance Violation Detected
AWS Config evaluated the resource and flagged the bucket as **NON-COMPLIANT**.

![Noncompliant](screenshots/08-config-noncompliant.png)

---

## Step 9 – GuardDuty Monitoring Enabled
GuardDuty was enabled to provide continuous threat detection using CloudTrail and DNS telemetry.

![GuardDuty Enabled](screenshots/09-guardduty-enabled.png)

---

# 🛠️ Incident Response & Remediation

---

## Step 10 – Public Bucket Policy Removed
The permissive bucket policy was deleted to eliminate anonymous access.

![Policy Removed](screenshots/10-policy-removed.png)

---

## Step 11 – Block Public Access Restored
Block Public Access was re-enabled to prevent future exposure.

![Block Public Access On](screenshots/11-block-public-access-on.png)

---

## Step 12 – Access Verification
Public access attempts now return an AccessDenied error, confirming remediation.

![Access Denied](screenshots/12-public-url-accessdenied.png)

---

## Step 13 – Compliance Restored
AWS Config re-evaluated the resource and confirmed **COMPLIANT** status.

![Compliant](screenshots/13-config-compliant.png)

---

# ✅ Final Outcome
- Public data exposure successfully identified  
- Audit logging validated via CloudTrail  
- Misconfiguration detected through AWS Config  
- Continuous monitoring established using GuardDuty  
- Manual remediation restored compliance  

---

## Key Security Takeaways
- Public cloud storage remains a leading cause of data breaches  
- Continuous monitoring is critical for early detection  
- CloudTrail provides essential forensic visibility  
- AWS Config enables scalable compliance enforcement  
- GuardDuty enhances threat context during investigations  
- Manual remediation prevents unintended automation risk  

---

## Disclaimer
This project was conducted in a controlled lab environment for educational purposes only.
No real customer data was used, and no production systems were tested.
