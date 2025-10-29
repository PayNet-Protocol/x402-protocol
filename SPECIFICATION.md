# x402 Protocol Specification
HTTP 402-based payment protocol for AI agents and APIs.
## Overview
The x402 protocol enables instant, programmatic payments using the HTTP 402 "Payment Required" status code and blockchain transactions.
## Protocol Flow
### 1. Client Requests Resource (No Payment)
```http
GET /api/protected HTTP/1.1
Host: api.example.com
2. Server Responds with 402 Payment Required
HTTP/1.1 402 Payment Required
Content-Type: application/json
{
  "amount": "1000000",
  "network": "solana",
  "token": "USDC",
  "recipient": "wallet_address_here"
}
3. Client Creates Blockchain Transaction
Client sends USDC to the recipient address on specified network.

4. Client Retries with Payment Proof
GET /api/protected HTTP/1.1
Host: api.example.com
X-Payment: {"hash":"tx_hash","amount":"1000000","network":"solana","token":"USDC"}
5. Server Verifies and Grants Access
HTTP/1.1 200 OK
Content-Type: application/json
{
  "data": "Premium content here"
}
Headers
X-Payment Header
Contains transaction proof as JSON string:

{
  "hash": "blockchain_transaction_hash",
  "amount": "1000000",
  "network": "solana|base|polygon|avalanche",
  "token": "USDC"
}
Supported Networks
Solana - Mainnet, USDC SPL token
Base - Mainnet, USDC ERC-20
Polygon - Mainnet, USDC ERC-20
Avalanche - C-Chain, USDC ERC-20
Reference Implementation
See PayNet Facilitator for production-ready implementation.

Demo
Try it live: https://paynet.network/demo

Click **"Commit new file"**
### **Step 5:** Also update README - click README.md, click pencil, paste:
```markdown
# x402 Protocol
> HTTP 402-based payment protocol for AI agents and APIs
The x402 protocol enables instant, programmatic payments using blockchain transactions and the HTTP 402 status code.
## Documentation
- [Protocol Specification](SPECIFICATION.md) - Complete protocol details
- [Reference Implementation](https://github.com/PayNet-protocol/paynet-facilitator) - Production code
## Quick Example
```javascript
// Server returns 402 with payment requirements
// Client makes blockchain transaction
// Client retries with X-Payment header
// Server verifies and grants access
Links
Live Demo: https://paynet.network/demo
Documentation: https://paynet.network/documentation
Quick Start: https://paynet.network/quickstart
License
Apache 2.0
