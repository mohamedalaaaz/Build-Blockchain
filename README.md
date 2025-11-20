Go Blockchain – Full Node + Wallet + API Server

A fully functional Proof-of-Work blockchain written in Go, including:

Blockchain core

Wallet system (ECDSA)
<img width="1536" height="1024" alt="ChatGPT Image Nov 20, 2025, 02_05_08 AM" src="https://github.com/user-attachments/assets/8c0ca14e-969d-47de-8283-7d184da5609a" />

Mining engine<img width="1536" height="1024" alt="ChatGPT Image Nov 20, 2025, 02_03_36 AM" src="https://github.com/user-attachments/assets/4f41800c-0f5a-41e5-aff6-b969060960b0" />

![Uploading ChatGPT Image Nov 20, 2025, 02_03_07 AM.png…]()

REST API server

Peer discovery

Consensus (Longest Chain Rule)

Transaction pool + broadcasting

CLI utilities

📌 Features
Feature	Description
Proof-of-Work (SHA-256)	Adjustable mining difficulty, secure PoW
Full Wallet System	ECDSA private/public keys, wallet address, signing
REST API	Get chain, submit transactions, mine blocks, check balances
Peer Discovery	Nodes automatically find each other on the network
Consensus Algorithm	Longest valid chain wins
Mining Rewards	Automatic mining reward to miner wallet
Transaction Pool	Pending transactions broadcasted to neighbors
Multiple Nodes	Run unlimited blockchain nodes with unique ports
🏗 Project Structure
/goblockchain
 ├── block/
 │    └── blockchain.go       # Core blockchain + transactions + PoW + consensus
 ├── wallet/
 │    └── wallet.go           # Wallet, private key, public key, signatures
 ├── utils/
 │    └── utils.go            # Signature helpers, key parsing, discovery
 ├── blockchain_server.go     # HTTP blockchain node server
 └── go.mod / go.sum

🌐 API Endpoints
Blockchain
Method	Endpoint	Description
GET	/	Returns full blockchain
GET	/amount?blockchain_address=	Get balance of an address
Transactions
Method	Endpoint	Description
GET	/transactions	List unconfirmed transactions
POST	/transactions	Create a new transaction
PUT	/transactions	Add transaction received from neighbor
DELETE	/transactions	Clear transaction pool
Mining
Method	Endpoint	Description
GET	/mine	Mine one block
GET	/mine/start	Start auto-mining loop
Consensus
Method	Endpoint	Description
PUT	/consensus	Sync with neighbors & replace chain if needed
🚀 How to Run a Node
1. Start a blockchain node
go run blockchain_server.go 5000


Then open:

http://localhost:5000/


To run multiple nodes:

go run blockchain_server.go 5001
go run blockchain_server.go 5002


Nodes will automatically sync with each other.

🔑 Create a Wallet
go run wallet.go


Output includes:

Private Key

Public Key

Blockchain Address

Use these to create signed transactions.

💸 Create a Transaction

Send:

POST /transactions
{
  "sender_blockchain_address": "YOUR_SENDER_WALLET",
  "recipient_blockchain_address": "RECIPIENT_WALLET",
  "sender_public_key": "HEX_PUBLIC_KEY",
  "value": 2.5,
  "signature": "SIGNATURE_HEX"
}


If the transaction signature is valid → added to pool and broadcasted.

⛏ Mine a Block

Manual mining:

GET /mine


Automatic mining loop:

GET /mine/start


Reward is sent to the node’s miner wallet.

🧠 Consensus Mechanism

Nodes compare chains from neighbors using:

Hash validation

Previous hash linking

Proof-of-work validation

The node will automatically adopt the longest valid chain.

🔌 Peer Discovery

Each node scans the local IP + port range:

5000 → 5003


And builds a neighbor list automatically.

🏦 Check Wallet Balance
GET /amount?blockchain_address=YOUR_ADDRESS


Returns:

{ "amount": 12.0 }

📄 Example JSON Response (Blockchain)
{
  "chain": [
    {
      "timestamp": 1732041021000,
      "nonce": 391,
      "previous_hash": "000...",
      "transactions": [
        {
          "sender_blockchain_address": "Address1",
          "recipient_blockchain_address": "Address2",
          "value": 1.5
        }
      ]
    }
  ]
}

🛠 Build for Production
go build -o blockchain_node blockchain_server.go
./blockchain_node 5000



📜 License

This project is open-source under the MIT License.
