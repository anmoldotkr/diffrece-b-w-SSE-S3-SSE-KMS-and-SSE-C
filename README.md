# diffrece-b-w-SSE-S3-SSE-KMS-and-SSE-C

When to Use Which Server-Side Encryption (SSE)
1. SSE-S3 (Server-Side Encryption with Amazon S3-Managed Keys)
When to Use: This is your default choice when you need encryption at rest, and the security or regulatory compliance requirements do not require an auditable log of who used the encryption key to access the data. It's the simplest and most cost-effective option.

How it Works: S3 handles everything. It generates a unique data key for your object, encrypts the key with a regularly rotated master key, and stores both.

2. SSE-KMS (Server-Side Encryption with AWS KMS Keys)
When to Use: You must use this when you need to meet strict compliance or security requirements that demand an audit trail of every decryption event. It's ideal for confidential financial or medical data where you need to prove who accessed the key and when.

How it Works: S3 sends a request to the AWS Key Management Service (KMS) to encrypt the data key. Every time the data is accessed, S3 calls KMS to decrypt the data key. Crucially, every KMS API call is logged in AWS CloudTrail, providing the required audit trail. This is the solution required by your scenario.

3. SSE-C (Server-Side Encryption with Customer-Provided Keys)
When to Use: You use this when your organization has a policy that mandates you provide and manage the actual encryption keys yourself, and you cannot store those keys in AWS KMS. You must send a secure hash of your key in the header of every PUT and GET request.

How it Works: AWS S3 encrypts and decrypts your data using the key you provide. S3 does not store your key; it stores a hash to validate future requests. Since the key is provided by you, S3 cannot automatically rotate it. You are responsible for key rotation and lifecycle management.
