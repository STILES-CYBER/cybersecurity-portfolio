 # Domain 1 — General Security Concepts

## 1.1 Security Controls

### Three Categories
- Technical — technology-based controls (firewalls, encryption, antivirus)
- Physical — physical barriers (fences, locks, CCTV, security guards)
- Administrative — policies and procedures (security policies, training, audits)

### Six Functional Types
- Preventive — stops attack before it happens (firewall, lock, MFA)
- Detective — identifies attack in progress (IDS, CCTV, log monitoring)
- Corrective — fixes damage after attack (backups, patches, incident response)
- Deterrent — discourages attackers (warning signs, security cameras, lighting)
- Compensating — alternative when primary control fails (MFA when password is weak)
- Directive — policies and rules staff must follow (acceptable use policy, NDAs)

### Key Examples
- Firewall = Technical + Preventive
- CCTV = Physical + Detective
- Security Policy = Administrative + Directive
- Backup = Corrective
- Fence = Physical + Deterrent

## 1.2 Cryptography

### Key Terms
- Encryption — converting plaintext to unreadable ciphertext
- Decryption — converting ciphertext back to plaintext
- Key — secret value used to encrypt and decrypt data
- Algorithm — mathematical process used for encryption

### Types of Encryption
- Symmetric — same key for encryption and decryption (fast, good for large data)
  - Examples: AES, DES, 3DES
- Asymmetric — public key encrypts, private key decrypts (slower, good for key exchange)
  - Examples: RSA, ECC, Diffie-Hellman

### Hashing
- One-way process — cannot be reversed
- Used to verify integrity of data
- Examples: MD5, SHA-1, SHA-256, SHA-3
- MD5 and SHA-1 are considered weak — SHA-256 preferred

### Key Lengths
- Longer key = stronger encryption
- AES-128 = good, AES-256 = stronger, industry standard

## 1.3 Authentication

### Authentication Types
- Something you know — password, PIN
- Something you have — smart card, token, phone
- Something you are — fingerprint, retina, face (biometrics)
- Somewhere you are — location-based
- Something you do — typing pattern, behaviour

### Multi-Factor Authentication (MFA)
- Combines two or more authentication types
- Example: password + phone OTP = MFA
- Two-factor authentication (2FA) = subset of MFA

### Authentication Protocols
- LDAP — directory-based authentication
- RADIUS — remote access authentication
- TACACS+ — Cisco device authentication
- Kerberos — ticket-based Windows authentication
- SAML — web-based single sign-on (SSO)

## Key Terms to Remember
- CIA Triad — Confidentiality, Integrity, Availability
- Non-repudiation — proof that someone performed an action
- AAA — Authentication, Authorization, Accounting
- PKI — Public Key Infrastructure
- Certificate Authority (CA) — issues digital certificates
- Digital Signature — proves authenticity and integrity of a message

## Practice Questions
1. Which encryption type uses the same key for encryption and decryption?
   Answer: Symmetric

2. Which hashing algorithm is considered most secure?
   Answer: SHA-256 or SHA-3

3. A password combined with a fingerprint is an example of?
   Answer: Multi-Factor Authentication (MFA)

4. Which control type fixes damage after an attack?
   Answer: Corrective

5. What does CIA stand for in cybersecurity?
   Answer: Confidentiality, Integrity, Availability
