# Submission for the Mammothon 2025

## Prism Passport
- Intro
  Prism Passport is a simple application where users can link their social accounts to a wallet and create a passport for themselves. The passport is secured by [Prism](https://x.com/prism_xyz) and [Reclaim protocol](https://reclaimprotocol.org/) so that no one, including the service provider can maliciously replace their identity without being detected.

  Prism Passport is participaing in the [Web Proof](https://docs.prism.rs/mammothon/reclaim.html) categry for the Mammothon 2025

- Demo site: https://mammothon-fe-umber.vercel.app/
- Source code:
  - [Frontend Website](https://github.com/tentou-tech/mammothon-fe)
  - [Backend Service](https://github.com/tentou-tech/prism-be)
- Features:
  - Account creation with wallet address and signature verification
  - Key management for accounts
  - Data storage with signature verification
  - Health check endpoint
- How it works
```mermaid
sequenceDiagram
    participant User
    participant FE as Frontend
    participant BE as Backend
    participant DA as Data Availability
    participant P as Reclaim Protocol

    User->>FE: Create account
    FE->>BE: Request create account payload
    FE->>FE: Sign payload with private key
    FE->>BE: Broadcast signed transaction (Prism)
    BE->>BE: Check if account exists (Prism)
    BE->>DA: Send transaction to Data Availability (Prism)

    User->>FE: Add data to account
    FE->>P: Request Verification
    P-->>FE: Reclaim Verification QR code
    FE-->>User: Reclaim Verification QR code
    FE->>P: Verify Account information
    P-->>FE: Verified user data
    FE->>BE: Request add data payload
    FE->>FE: Sign payload and Verified user data with private key
    FE->>BE: Broadcast signed transaction (Prism)
    BE->>BE: Check if account exists (Prism)
    BE->>DA: Send transaction to Data Availability (Prism)

    User->>FE: Get account
    FE->>BE: Call to backend to get account
    BE->>DA: Call to Data Availability to get account (Prism)

    User->>FE: Get all accounts
    FE->>BE: Call to backend to get all accounts
    BE->>BE: Get all accounts from database (Prism)
```
- Demo Video: https://www.loom.com/share/e860dbd8b9e94ba9abfc37e1b7a6829e?sid=a7091af8-94c8-4a76-a8f1-c4c586e6d6c1


