# 🔐 AWS Security Cheat Sheet

This guidance is my own and does not represent the views, guidance, or recommendations from any employer. I have put this list together from my personal experience.

A comprehensive guide to securing AWS environments, covering IAM, network security, data protection, monitoring, and compliance. 🛡️

---

## 🆔 1. Identity and Access Management (IAM)

| Best Practice | Description |
|--------------|-------------|
| ✅ **Use IAM Roles** | Avoid static credentials; assign IAM roles to applications instead. |
| 🎯 **Least Privilege Access** | Grant only necessary permissions to users and services. |
| 🔑 **Enable MFA** | Require Multi-Factor Authentication for all IAM users. |
| 🔗 **Service-Linked Roles** | Use AWS service-linked roles for secure service-to-service communication. |
| 🔄 **Rotate IAM Credentials** | Regularly rotate access keys and IAM credentials. |
| 🔐 **Enforce Strong Passwords** | Set password policies for complexity, rotation, and expiration. |
| 🔍 **IAM Access Analyzer** | Detect overly permissive policies to minimize risk. |

---

## 🌐 2. Network Security

| Best Practice | Description |
|--------------|-------------|
| 🏗 **Use VPCs** | Isolate and segment workloads using Virtual Private Clouds. |
| 🛡 **Enable AWS WAF** | Protect applications from common web threats. |
| 🚧 **Restrictive Security Groups** | Limit inbound and outbound traffic to required sources only. |
| 🛑 **Network ACLs (NACLs)** | Apply additional layer of security beyond Security Groups. |
| ⚡ **AWS Shield** | Protect against DDoS attacks (Standard for free, Advanced for more protection). |
| 📊 **VPC Flow Logs** | Enable logging to monitor network traffic and detect anomalies. |

---

## 🔒 3. Data Security

| Best Practice | Description |
|--------------|-------------|
| 🔐 **Encrypt Data at Rest** | Use AWS KMS (Key Management Service) for secure encryption. |
| 📡 **Encrypt Data in Transit** | Ensure HTTPS/TLS encryption for all data transmissions. |
| 🕵️ **Secrets Management** | Store credentials securely in AWS Secrets Manager or SSM Parameter Store. |
| 💾 **Automated Backups** | Use AWS Backup or snapshots to maintain data redundancy. |
| 🚫 **S3 Bucket Policies** | Enforce least privilege and block public access to sensitive data. |
| 🔄 **S3 Object Lock & Versioning** | Prevent accidental deletion and enable recovery options. |

---

## 📊 4. Monitoring & Logging

| Best Practice | Description |
|--------------|-------------|
| 🔍 **Enable CloudTrail** | Track API calls and changes across AWS accounts. |
| 📈 **Monitor with CloudWatch** | Set up alarms and logs for performance & security events. |
| ✅ **Use AWS Config** | Audit configuration changes for compliance and security. |
| 🛡 **Enable GuardDuty** | Detect anomalies, threats, and potential security breaches. |
| 🏛 **AWS Security Hub** | Aggregate security findings in one dashboard. |
| 📢 **Set Up SNS Alerts** | Get real-time notifications for security-related events. |

---

## 🖥️ 5. Instance & Compute Security

| Best Practice | Description |
|--------------|-------------|
| 🚫 **Use Instance Profiles** | Avoid storing AWS credentials on EC2 instances. |
| 🔄 **Patch EC2 Instances** | Regularly update OS and software for security fixes. |
| 🔒 **Restrict SSH Access** | Limit SSH connections via Security Groups and IAM rules. |
| 🕵️ **Run AWS Inspector** | Perform vulnerability assessments on EC2 instances. |
| 👤 **Disable Root Logins** | Use IAM and sudo for administrative access instead. |

---

## 📦 6. Serverless & Application Security

| Best Practice | Description |
|--------------|-------------|
| 🔐 **Enforce Least Privilege for Lambda** | Assign minimal permissions to Lambda functions. |
| 🛠 **Scan Dependencies** | Use AWS CodeGuru and security scanners to check for vulnerabilities. |
| 🔑 **Secure API Gateway** | Use authentication (IAM, Cognito, JWT) for API endpoints. |
| 🆔 **Use Cognito for Authentication** | Manage secure user authentication with AWS Cognito. |
| 🔒 **Secure Database Access** | Prefer IAM authentication for RDS & DynamoDB over password-based access. |

---

## ⚖️ 7. Compliance & Best Practices

| Best Practice | Description |
|--------------|-------------|
| 📊 **AWS Well-Architected Tool** | Evaluate security best practices for AWS workloads. |
| 🏛 **Use Service Control Policies (SCPs)** | Enforce policies across multiple AWS accounts via AWS Organizations. |
| 🔍 **AWS Audit Manager** | Automate compliance tracking and reporting. |
| 🛠 **Understand the Shared Responsibility Model** | AWS secures infrastructure, customers secure applications. |
| 🤖 **Automate Compliance Checks** | Use AWS Config Rules to enforce security policies. |

---

## 🆘 8. Incident Response & Recovery

| Best Practice | Description |
|--------------|-------------|
| 🔄 **Test Incident Response Plans** | Regularly conduct security drills. |
| ⚡ **Automate Security Responses** | Use AWS Lambda and Security Hub for auto-remediation. |
| 💾 **Maintain Backups** | Regularly back up critical data and systems. |
| 🔍 **Review IAM Access Advisor** | Identify and remove unused permissions. |
| 🌎 **Enable Centralized Logging** | Use AWS Organizations for unified security monitoring. |

---

## 🎯 Summary: AWS Security Best Practices 🚀

- **🛑 IAM Security:** Enforce **MFA**, **least privilege access**, and **strong password policies**.
- **🛡 Network Security:** Secure VPCs with **Security Groups, NACLs, and AWS WAF**.
- **🔐 Data Security:** Encrypt data at **rest (AWS KMS) & in transit (TLS/SSL)**.
- **📊 Monitoring:** Use **CloudTrail, CloudWatch, GuardDuty, and Security Hub**.
- **🚀 Application Security:** Secure **Lambda, API Gateway, and RDS authentication**.
- **⚖️ Compliance:** Leverage **AWS Organizations, Audit Manager, and SCPs**.
- **🆘 Incident Response:** **Test plans, automate remediation, and maintain backups**.

🔥 **Security is a continuous process!** Keep refining your AWS security strategies and follow best practices for a resilient cloud environment. 🚀
