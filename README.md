# ZKCertify

This repository contains a **ZK-based** verification system that enables the generation and validation of attestations across multiple chains (EDUCHAIN and Arbitrum). The system also demonstrates how user data (like CGPA, test score) can be verified and minted into an NFT on the chosen chain.

## Table of Contents
- [Overview](#overview)
- [Core Idea](#core-idea)
- [Demo](#demo)
- [Architecture](#architecture)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Environment Variables](#environment-variables)
- [Running Locally](#running-locally)
- [Usage](#usage)
- [Future Plans](#future-plans)
- [License](#license)

---

## Overview
ZKCertify leverages **zero-knowledge proofs** to ensure the integrity of user data without exposing the underlying information. It allows recruiters or other parties to:

1. Request verification of a user's credentials (CGPA, test scores).
2. Generate and validate ZK proofs.
3. Mint an NFT as proof of verification on the selected chain (Arbitrum or EDUCHAIN).

---

## Core Idea
The core idea behind **ZKCertify** is to create a transparent yet privacy-preserving platform for **students** and **recruiters**:

1. **Student Registration & Data Storage**  
   - Students register on the platform and provide their **CGPA**.  
   - As they learn new skills, they can take various **tests** on the platform.

2. **Scoring & Verification**  
   - Each student’s CGPA and newly acquired **test scores** are combined to check if they exceed a certain **threshold**.  
   - If the sum is greater than the threshold, the platform records a **1** (pass), otherwise a **0** (fail).  
   - This pass/fail outcome is then **verified** on-chain using **ZK proofs**, ensuring that the underlying data (CGPA, test score) remains private.

3. **Recruiter Verification**  
   - When a student applies for a role, the recruiter can easily verify the student's performance by checking the on-chain proof.  
   - The **NFT** minted from this verification process serves as a **tamper-proof attestation** of the student’s credentials.

---

## Demo
**Video Demo:**  
https://youtu.be/YG1DjKzlmFQ  

# Screenshots

## Landing Page  
![Landing Page](https://github.com/user-attachments/assets/f2da6a85-c299-48d8-970d-8c33a69ff07c)

## Recruiter Dashboard  
![Recruiter Dashboard](https://github.com/user-attachments/assets/bfd08cda-6a1c-4202-a02a-efa206582556)

## Verification Page  
![Verification Page](https://github.com/user-attachments/assets/5b969f9b-6c0a-4505-a864-8dcedb614e1c)

## Skill Assessment via AI  
![Skill Assessment via AI](https://github.com/user-attachments/assets/05cadecb-23a3-4253-a885-9e965b092425)

## AI-Generated Test  
![AI-Generated Test](https://github.com/user-attachments/assets/f8d99b82-a0e4-418f-b3aa-072f53e6944e)

## Student Profile  
![Student Profile](https://github.com/user-attachments/assets/cae80960-b87a-42f3-b11a-26a24d615ee0)

## Arbitrum Sepolia  
![Arbitrum Sepolia](https://github.com/user-attachments/assets/52a3679e-93f4-4d1a-afab-bb72b008e29b)

## EduChain  
![EduChain](https://github.com/user-attachments/assets/7b3f6fcd-7d4a-4fcd-9f02-ae5a0adb7f48)

## Deployed Backend  
![Deployed Backend](https://github.com/user-attachments/assets/a0808b42-35b7-4421-b725-937ed12d11fa)


## Architecture
Below is a high-level architecture diagram illustrating the major components and data flow:

![image](https://github.com/user-attachments/assets/5e6e2ba9-7d71-4181-b683-5bd43fa8097c)
![image](https://github.com/user-attachments/assets/611bf317-9b22-4ef7-8be9-43fb3183c0a2)


- **User (Student)** can:
  - Connect/disconnect wallet (e.g., MetaMask).
  - Add CGPA and take tests (which updates verification data).
  - Generate proofs of credentials.
- **Recruiter** can:
  - Connect wallet.
  - Request verification of a student’s credentials.
  - Receive the final attestation (NFT) minted on the chain of choice (Arbitrum or EDUCHAIN).

---

## Prerequisites
- **Node.js** (>= 14.x recommended)
- **npm** (>= 6.x)
- **Circom** (for ZK circuit compilation)
- **MetaMask** (browser extension) for testing the dApp

---

## Installation

1. **Clone the Repository**  
   ```bash
   git clone https://github.com/bansalayush2407/ZKCertify.git
   cd ZKCertify
   ```

2. **Install Dependencies**  
   - **Backend**:
     ```bash
     cd backend
     npm install
     ```
   - **Frontend**:
     ```bash
     cd ../frontend
     npm install
     ```

3. **Compile ZK Circuit**  
   Return to the root folder (or wherever your `circuit.circom` file is located) and run:
   ```bash
   npm run complete-circuit
   ```
   This command will:
   - Compile your circuit.
   - Generate the necessary proving and verification keys.
   - Create the witness.

4. **Deploy the zkCertify Contract**  
   You need to deploy the **zkCertify Contract** on both **EDUCHAIN** and **Arbitrum**. Once deployed, update your environment variables with the addresses:
   ```
   EDU_ZKVERIFY_CONTRACT_ADDRESS="0x147AD899D1773f5De5e064C33088b58c7acb7acf"
   ARB_ZKVERIFY_CONTRACT_ADDRESS="0x82941a739E74eBFaC72D0d0f8E81B1Dac2f586D5"
   VK_HASH="0xa0e25c80bfa3f16a1f2a971730011a85066bc21027722662136a24fa59a59297"
   ```
   > **Note:** `VK_HASH` is generated by the function in `circuit/setup/hash.js`.

---

## Environment Variables
Create a `.env` file in the **`/backend`** directory and add the following entries:
```
ZKV_RPC_URL=
ETH_RPC_URL=

ETH_ZKVERIFY_CONTRACT_ADDRESS=
ARB_ZKCERTIFY_CONTRACT_ADDRESS=
EDU_ZKCERTIFY_CONTRACT_ADDRESS=

GROQ_API_KEY=
ZKV_SEED_PHRASE=
ETH_SECRET_KEY=

ARB_URL=
EDU_URL=
```
- **ZKV_RPC_URL**: The RPC endpoint for ZKV.  
- **ETH_RPC_URL**: The RPC endpoint for Ethereum (or your desired testnet).  
- **ETH_ZKVERIFY_CONTRACT_ADDRESS**: Address of the ZKVerify contract on Ethereum (if applicable).  
- **ARB_ZKCERTIFY_CONTRACT_ADDRESS**: Address of the contract deployed on Arbitrum.  
- **EDU_ZKCERTIFY_CONTRACT_ADDRESS**: Address of the contract deployed on EDUCHAIN.  
- **GROQ_API_KEY**: (If you use any third-party or internal API key).  
- **ZKV_SEED_PHRASE**: Seed phrase for the account used in the ZK environment.  
- **ETH_SECRET_KEY**: Private key for Ethereum-based deployments.  
- **ARB_URL**: RPC endpoint for Arbitrum.  
- **EDU_URL**: RPC endpoint for EDUCHAIN.

---

## Running Locally

1. **Backend**  
   ```bash
   cd backend
   npm install
   node app/src/index.js
   ```
   The backend should now be running on the specified port (default is usually `http://localhost:3001` or whichever is set in your code).

2. **Frontend**  
   ```bash
   cd ../frontend
   npm install
   npm run dev
   ```
   By default, this starts on `http://localhost:3000` (or the next available port).

---

## Usage
1. **Connect Wallet** (e.g., MetaMask) on the website.  
2. **Register as Student** to add your **CGPA**.  
3. **Take Tests** to generate or update your test scores.  
4. **Generate Proof** using the underlying **ZK circuit**, which checks if CGPA + test score ≥ threshold.  
5. **Select a Chain** (Arbitrum or EDUCHAIN) to mint the verification NFT.  
6. **Recruiters** can connect their wallets to verify your credentials on-chain and see proof of whether you passed the threshold.

---

## Special Feature
This project looks after a special feature of working on a combination of academics as well as skillset of a student. The CGPA portion looks after the academic proficiency of the student whereas the exam (here - MCQ based questions) tests the skillset of the student. 

Hence, a mixture of Online Assessment + Academic Proficiency both at the same time - allowing the student to prove his proficiency with a combined value (score) of his Academic performance as well as his skillset, to be eligible for hiring. 

Hence, a student who might not be much academically proficient but has a strong skillset holds an equal chance to be hired against a student who is academically good but might not have a very strong skillset.

---

## Future Plans
1. **Additional Skill Tests**  
   - Incorporate new test types (e.g., **Data Structures & Algorithms**, **Assignments**, **Interviews**) that can be automatically graded by **AI**.
2. **Job Postings and Matching**
   - Enable recruiters to post job openings with required skills.
   - Automatically **match** qualified students to open positions based on their CGPA + test scores.
3. **NFT-Based Resume**  
   - Allow students to generate a **resume as an NFT**, bundling their verified credentials in a single, on-chain artifact.
4. **Inculcating Real-World Data**
   - This project currently works on a sample dataset which can be replaced by a real time dataset containing actual (real-time) records of each and every student.
5. **Modifiable Cut-off (Threshold) Score**
   - This project currently considers a sample threshold value (equivalent to "Combined Score of a student in his/her test and his CGPA) of 'x' (here x=1400) which can be modified as per the requirements of the recruiter.

These enhancements will further streamline the student–recruiter interaction while maintaining privacy and trust via zero-knowledge proofs.

---
