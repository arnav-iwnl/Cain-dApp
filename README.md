# 🔐 Cain-dApp: Blockchain-Based Document Verification with IPFS

A secure, decentralized document verification system combining **Blockchain** and **IPFS** technologies. Store document hashes immutably on-chain while maintaining document privacy with encrypted IPFS storage.

![Status](https://img.shields.io/badge/status-active-brightgreen)
![License](https://img.shields.io/badge/license-MIT-blue)
![Built with](https://img.shields.io/badge/built%20with-Web3.js%20|%20Solidity%20|%20IPFS-blueviolet)

---

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [Architecture](#architecture)
- [File Structure](#file-structure)
- [Troubleshooting](#troubleshooting)
- [Security Considerations](#security-considerations)
- [License](#license)
- [Acknowledgments](#acknowledgments)

---

## 🎯 Overview

Cain-dApp is a Web3-powered decentralized application that solves document verification challenges in a trustless environment. By leveraging blockchain immutability and IPFS decentralization, the system ensures:

- **Authenticity**: Document hashes are permanently recorded on-chain
- **Integrity**: Tampered documents are immediately detected
- **Privacy**: Document content is encrypted and stored on IPFS, not the blockchain
- **Accessibility**: Authorized parties can retrieve and verify documents anytime

### How It Works

1. **Upload Phase**: Document is encrypted → hash stored on blockchain → file stored on IPFS
2. **Verification Phase**: Retrieve document from IPFS → decrypt → compute hash → compare with blockchain record
3. **Authorization**: Owner controls who can upload and verify documents

---

## ✨ Features

- ✅ **Secure Document Verification** using Blockchain and IPFS
- ✅ **Decentralized System** with no central point of failure
- ✅ **Zero-Intermediary Verification** requiring no third-party services
- ✅ **Intuitive Web Interface** for non-technical users
- ✅ **Multi-Format Support** for various document types
- ✅ **Role-Based Access Control** (Owner, Exporter, Verifier)
- ✅ **Document Encryption** for sensitive content
- ✅ **Real-Time Status Updates** with QR code generation
- ✅ **Network Agnostic** supports multiple EVM networks

---

## 🛠️ Tech Stack

| Component | Technology | Details |
|-----------|-----------|---------|
| **Frontend** | HTML5, CSS3, JavaScript ES6+ | Responsive UI with Bootstrap 5 |
| **Blockchain** | Solidity 0.8.x, Web3.js 1.7.0 | Smart contracts on Ethereum-compatible chains |
| **Storage** | IPFS via Pinata | Decentralized file storage with pinning |
| **Wallet** | MetaMask | User authentication & transaction signing |
| **Build Tools** | Node.js, npm | Dependencies: web3, dotenv, ipfs-api |
| **UI Components** | Bootstrap 5, AOS, PureCounter | Animations, counters, responsive design |
| **QR Codes** | qrcode.min.js | Generate verification QR codes |

---

## 📦 Prerequisites

Before you begin, ensure you have the following installed and configured:

- **Node.js** (v14 or higher) - [Download](https://nodejs.org/)
- **npm** (v6 or higher) - comes with Node.js
- **MetaMask Wallet** - [Install Extension](https://metamask.io/)
- **Pinata Account** - [Sign up free](https://pinata.cloud/) for IPFS pinning
- **Live Server Extension** (VS Code) - for local development
- **remix.ethereum.org** account for smart contract deployment

### Environment Requirements

- **Ethereum Sepolia Testnet** (default, can be configured to other EVM networks)
- Sepolia ETH for transaction fees (get free Sepolia testnet ETH via [faucets](https://sepoliafaucet.com/))
- Internet connection for IPFS (Pinata) and blockchain interaction

---

## 🚀 Installation

### Step 1: Install Dependencies

```bash
npm install
```

This installs required packages including Web3.js and any dependencies listed in `package.json`.

### Step 2: Deploy Smart Contract

1. Open [remix.ethereum.org](https://remix.ethereum.org/)
2. Create a new file and copy contents from `Contract/Verfication.sol`
3. Compile the contract (Compiler version: 0.8.0+)
4. Deploy to your desired network (Testnet recommended: Sepolia, Mumbai, etc.)
5. **Important**: Copy the deployed contract address

### Step 3: Configure Application

Edit `js/App.js` and update the following constants:

```javascript
// Pinata IPFS Configuration
const pinataJWT = "YOUR_PINATA_JWT_TOKEN"; // Get from Pinata dashboard

// Smart Contract Configuration
window.CONTRACT = {
  address: "0x...", // Paste your deployed contract address
  network: "https://ethereum-sepolia-rpc.publicnode.com", // Sepolia RPC (or your network)
  explore: "https://sepolia.etherscan.io", // Sepolia Explorer (or your network explorer)
  abi: [ /* ABI already provided */ ]
};
```

**How to get Pinata JWT Token:**
1. Go to [Pinata Dashboard](https://app.pinata.cloud/)
2. Click "API Keys" in the top left
3. Create a new API key
4. Copy the JWT token and paste it in `App.js`

**How to change networks:**
- Update `network` URL for your desired RPC endpoint
- Update `explore` URL for the corresponding block explorer
- Network is auto-detected by MetaMask; ensure your wallet matches the configured network

### Step 4: Start Development Server

**Using VS Code Live Server:**
1. Install "Live Server" extension
2. Right-click on `index.html`
3. Select "Open with Live Server"
4. Access at `http://localhost:5500`

**Using Python (alternative):**
```bash
python -m http.server 8000
# Visit: http://localhost:8000
``` Details

### Smart Contract Configuration

The Solidity contract (`Contract/Verfication.sol`) includes:

1. **Owner Functions**: Manage authorized exporters
2. **Exporter Functions**: Upload and manage documents
3. **Verifier Functions**: Retrieve and verify document authenticity
4. **Storage**: Uses blockchain for hashes and metadata

After deployment, copy the contract address and paste it in `js/App.js`.

### Pinata IPFS Configuration

Documents are uploaded to IPFS via Pinata:

1. All files are first uploaded to Pinata IPFS
2. IPFS Content Identifier (CID) is returned
3. CID and document hash are stored on blockchain
4. Documents can be retrieved from IPFS gateway: `https://ipfs.io/ipfs/{CID}`

```javascript
const pinataJWT = "YOUR_JWT_TOKEN"; // Required for uploads
```

---

## 📖 Usage

### For Document Owners/Admins

###Navigate to "Upload" page
2. Connect wallet (MetaMask)
3. Select document file (PDF, DOCX, TXT, etc.)
4. Click "Hashing Your Document" (generates SHA3 hash)
5. Click "Upload Document" to complete
```

**Process:**
- Document is hashed locally using SHA3
- File is uploaded to IPFS via Pinata
- IPFS CID received and stored
- Document hash + CID + metadata stored on blockchain
- Transaction receipt displayed with confirmation

**What gets stored:**
- ✅ Document hash (SHA3) → Blockchain
- ✅ IPFS CID (content identifier) → Blockchain  
- ✅ Actual document file → IPFS (decentralized)
- ✅ Exporter info & timestamp → Blockchain

#### Supported Formats
- **Documents**: PDF, DOCX, DOC, TXT
Two ways to verify:

**Method 1: Direct Verification**
```
1. Navigate to "Verify" page
2. Select document from dropdown or enter hash
3. Click "Verify Document"
4. System retrieves from IPFS and compares hash
```

**Method 2: URL/QR Code**
```
1. Receive verification link with hash parameter
2. Click link (e.g., verify.html?hash=0x...)
3. Document automatically verified
4. Result displayed with full details
```

**Verification Result:**
- ✅ **Authentic**: Hash matches blockchain record → Document is genuine
- ❌ **Tampered**: Hash mismatch → Document has been altered
- ⚠️ **Not Found**: Document not in system

**Displayed Information:**
- Document hash (SHA3)
- IPFS CID and download link
- Exporter information
- Upload timestamp & block number
- Transaction hash on blockchain

#### Generate QR Code

After verification, you can:
- Click "Generate QR Code" to create a shareable QR
- QR points to IPFS document for public access
- Share with others for instant verification
- QR download option availabl
- Document metadata saved

#### Supported Formats
- PDF (.pdf)
- Documents (.docx, .doc, .txt)
- Spreadsheets (.xlsx, .xls, .csv)
- Images (.png, .jpg, .jpeg)

### For Verifiers

#### ✅ Verify Documents

```
1. Click "Verify" in navigation
2. Select document from dropdown
3. Review document details
4. Click "Verify"
```

**Verification Process:**
- Retrieves document from IPFS
- Decrypts document locally
- Computes hash of retrieved document
- Compares with blockchain-stored hash
- Displays: ✅ Authentic or ❌ Tampered

#### Generate QR Code

- Click "Generate QR Code" after verification
- Share QR code with others for quick verification link
- QR code encodes document hash for easy reference

---

## 🏗️ Architecture

### System Components

```
┌─────────────────────────────────────────┐
│         Frontend (HTML/CSS/JS)          │
│  (User Interface & Interactions)        │
└──────────┬──────────────────────────────┘
           │
    ┌──────┴──────┬──────────────┐
    │             │              │
    ▼             ▼              ▼
┌─────────┐ ┌──────────┐  ┌──────────┐
│Blockchain│ │   IPFS   │  │Encryption│
│(Contract)│ │(Storage) │  │  Engine  │
└─────────┘ └──────────┘  └──────────┘
    │             │
    └─────────────┴──────────────┘
           (Web3.js)
```

### Data Flow

**Upload:**
```
Document → Encrypt → IPFS → Store (CID, Hash) → Blockchain
```

**Ver❌ "MetaMask not detected" or "Connect Wallet" not working
- ✅ Install [MetaMask extension](https://metamask.io/)
- ✅ Refresh page (F5)
- ✅ Check MetaMask icon in toolbar - make sure extension is enabled
- ✅ Allow dApp to access MetaMask (check browser warnings)
- ✅ Try incognito mode (might have extension conflicts)

#### ❌ "Contract address undefined" error
- ✅ Open `js/App.js` and verify `CONTRACT.address` is set to valid contract address
- ✅ Ensure contract is deployed to the same network as MetaMask
- ✅ Check contract was successfully deployed in Remix
- ✅ Contract address should start with `0x`

#### ❌ "IPFS upload fails" or "Pinata Error"
- ✅ Check Pinata JWT token in `js/App.js` (should not be `"//"`)
- ✅ Verify Pinata account is active at [pinata.cloud](https://pinata.cloud/)
- ✅ Check file size (recommended < 100MB)
- ✅ Verify internet connection is stable
- ✅ Check browser console (F12) for exact error message

#### ❌ "Wrong Network" error
- ✅ Open MetaMask
- ✅ Switch to **Sepolia** testnet (or your configured network)
- ✅ Refresh the page
- ✅ If network missing, add it manually in MetaMask settings
- ✅ RPC URL: `https://ethereum-sepolia-rpc.publicnode.com`

#### ❌ "Insufficient Balance" during transaction
- ✅ Ensure wallet has Sepolia ETH
- ✅ Get free testnet ETH from [Sepoliafaucet.com](https://sepoliafaucet.com/)
- ✅ Wait for faucet transaction to complete
- ✅ Check balance in MetaMask

#### ❌ "Gas Estimation Failed"
- ✅ Increase gas limit manually in transaction modal
- ✅ Ensure adequate wallet balance
- ✅ Try transaction again after a few minutes
- ✅ Check if contract is correctly deployed

#### ❌ "Document not found" after verification
- ✅ Verify document was successfully uploaded (check transaction receipt)
- ✅ Check IPFS status at [IPFS.io](https://ipfs.io/)
- ✅ Wait 30-60 seconds for IPFS network propagation
- ✅ Try accessing directly: `https://ipfs.io/ipfs/{CID}`

####**Blockchain-verified hashes** - Document integrity guaranteed by Smart Contract
- ✅ **Immutable records** - All documents permanently recorded on blockchain
- ✅ **MetaMask integration** - Secure wallet-based authentication
- ✅ **Role-based access control** - Owner, Exporter, and Verifier roles
- ✅ **Decentralized storage** - Files stored on IPFS, not centralized servers
- ✅ **Client-side hashing** - SHA3 hashing done locally, not on servers

### Known Limitations

⚠️ **Current Version (Development):**

- Document content is **not encrypted** - stored in plaintext on IPFS
- No **rate limiting** on uploads - vulnerable to spam
- Minimal **input validation** - rely on browser checks
- Full contract/metadata visible on blockchain - privacy concerns
- No **document expiration** mechanism

### Production Recommendations

🚀 **Before deploying to mainnet:**

1. **Smart Contract Audit** 
   - Professional security audit by blockchain security firm
   - Test against known exploits (reentrancy, overflow, etc.)
   - Gas optimization and cost reduction

2. **Document Encryption**
   - Implement AES-256 encryption before IPFS upload
   - Secure key management (consider key derivation)
   - Add document access control

3. **Secrets Management**
   - Never commit `.env` files to git
   - Use `.gitignore` to exclude sensitive files
   - Store secrets in environment variables only
   - Rotate Pinata API keys regularly

4. **Network Security**
   - **HTTPS only** - never use HTTP in production
   - Enable CORS restrictions
   - Implement rate limiting on uploads
   - Add request validation and sanitization

5. **Access Control**
   - Implement multi-signature for owner functions
   - Add exporter approval workflow
   - Implement document expiration/deletion
   - Add user permissions system

6. **Monitoring & Backup**
   - Monitor contract for unusual activity
   - Regular backup of important data
   - Error logging and alerting system
   - Transaction monitoring

### Best Practices

```javascript
// ✅ DO:
- Use hardware wallets (Ledger, Trezor) for owner accounts
- Implement function-level access controls
- Keep dependencies updated: npm audit fix
- Test thoroughly on testnet before mainnet
- Log all transactions for audit trails

// ❌ DON'T:
- Expose error messages with sensitive info
- Trust unvalidated user input
- Use development keys in production
- Store private keys in code repositories
- Override security warnings in MetaMask
```

### Audit Checklist

- [ ] Contract audited by professional firm
- [ ] All private keys secured
- [ ] HTTPS enabled
- [ ] Rate limiting implemented
- [ ] Input validation on all functions
- [ ] Document encryption enabled
- [ ] Multi-sig for critical functions
- [ ] Monitoring and logging in place
- [ ] Disaster recovery plan ready
- [ ] User documentation complete
└── assets/
    └── images/             # UI images and icons
```

---

## 🐛 Troubleshooting

### Common Issues & Solutions

#### "MetaMask not detected"
- ✅ Install MetaMask extension
- ✅ Refresh the page
- ✅ Check if MetaMask is authorized for the site

#### "Contract address undefined"
- ✅ Verify contract address in `js/App.js`
- ✅ Ensure address matches deployed network
- ✅ Contract must be deployed before using dApp

#### "IPFS upload fails"
- ✅ Check Infura API credentials
- ✅ Verify internet connection
- ✅ Check if file size exceeds limits
- ✅ Ensure Infura account is active

#### "Wrong network error"
- ✅ Open MetaMask
- ✅ Switch to the correct network
- ✅ Refresh the page
- ✅ Update RPC URL in `App.js` if needed

#### "Gas estimation failed"
- ✅ Ensure wallet has sufficient balance
- ✅ Check gas price settings
- ✅ Try with lower gas price on testnets

#### "Document not found in IPFS"
- ✅ Check IPFS node status
- ✅ Verify document wasn't corrupted
- ✅ Wait for IPFS network propagation

### Getting Help

- Check MetaMask Network Settings
- Verify contract deployment on network explorers
- Check browser console (F12) for error messages
- Review IPFS gateway status

---

## 🔒 Security Considerations

### Current Implementation

- ✅ Client-side encryption for documents
- ✅ Blockchain immutability for document hashes
- ✅ MetaMask wallet authentication
- ✅ Role-based access control

### Production Recommendations

⚠️ **Before deploying to mainnet:**

1. **Smart Contract Audit**: Have the Solidity contract audited by professionals
2. **Encryption**: Use industry-standard encryption (AES-256)
3. **Private Keys**: Never expose private keys or Infura secrets
4. **HTTPS Only**: Always use HTTPS in production
5. **Rate Limiting**: Implement API rate limits for IPFS uploads
6. **Access Control**: Strengthen authorization mechanisms
7. **Error Handling**: Avoid exposing sensitive information in errors

### Best Practices

- Store sensitive configuration in environment variables (`.env`)
- Use hardware wallets (Ledger, Trezor) for production
- Implement multi-signature contracts for critical functions
- Regular security audits and updates
- Keep Web3.js and dependencies updated

---



## 🙏 Acknowledgments

This project builds upon the work and documentation of:

- **Metamask** - [Documentation](https://docs.metamask.io/)
- **Solidity** - [Documentation](https://docs.soliditylang.org/)
- **Web3.js** - [Documentation](https://web3js.readthedocs.io/)
- **IPFS & Infura** - [Documentation](https://infura.io/docs)
- **Bootstrap** - For UI components

Special thanks to the Ethereum and IPFS communities for their continuous support and innovation.

---

## 📞 Support & Contributing

Found a bug? Have an improvement?

- **Create an Issue**: Report bugs or feature requests
- **Pull Requests**: Contributions are welcome!
- **Discussions**: Share ideas and feedback

---

**Last Updated**: April 2026 | **Status**: Active & Maintained



