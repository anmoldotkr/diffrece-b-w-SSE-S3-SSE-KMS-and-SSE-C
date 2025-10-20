# diffrece-b-w-SSE-S3-SSE-KMS-and-SSE-C

***

# 🔒 Amazon S3 Server-Side Encryption (SSE) Overview

Amazon S3 offers three mutually exclusive options for Server-Side Encryption (SSE), each defined by how the encryption keys are managed.

## 1. SSE-S3: S3-Managed Keys (The Default)

| Feature | Detail |
| :--- | :--- |
| **Key Management** | Amazon S3 manages and rotates the master key. |
| **Audit Trail** | **NO** audit trail in CloudTrail for key usage by individuals. |
| **Cost** | Free (no direct charge for the encryption process). |
| **When to Use** | Your **default choice** for encryption at rest where a detailed, auditable log of **who** used the key is **not** required by compliance. |
| **How It Works** | S3 handles all key operations internally: generating a unique data key for the object and encrypting that key with a regularly rotated master key. |

---

## 2. SSE-KMS: AWS KMS Keys (The Auditable Choice)

| Feature | Detail |
| :--- | :--- |
| **Key Management** | AWS **KMS** manages the key (Customer-Managed Key or AWS-Managed Key). |
| **Audit Trail** | **YES** - Every key operation (encrypt/decrypt) is logged in **AWS CloudTrail**, providing a clear audit trail of who used the key. |
| **Cost** | Low cost per API call to KMS for encryption/decryption requests. |
| **When to Use** | When strict **compliance** (e.g., HIPAA, PCI-DSS) or **security requirements** demand an **auditable log** of every decryption event. Ideal for confidential financial or medical data. |
| **How It Works** | S3 requests KMS to encrypt/decrypt the object's data key. The security benefits come from the fact that **KMS API calls are logged**. |

---

## 3. SSE-C: Customer-Provided Keys (The External Key Choice)

| Feature | Detail |
| :--- | :--- |
| **Key Management** | **You** provide and manage the actual encryption key externally. |
| **Audit Trail** | **NO** audit trail within AWS services like CloudTrail. |
| **Key Rotation** | **Your responsibility** (manual). S3 cannot automatically rotate the key. |
| **When to Use** | When your organization's policy mandates that **you must control the encryption key** and prevent it from being stored in **AWS KMS**. |
| **How It Works** | You must send a secure hash of your key in the header of every PUT and GET request. S3 uses the key for the session but **does not store the key itself**. |

***
