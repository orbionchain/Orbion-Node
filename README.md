# Orbion Node Validator: A Complete Guide for Beginners 🚀

Welcome\! This guide is designed to walk you through the process of setting up an **Orbion Validator Node** from scratch. We'll explain every step, what each command does, and how to ensure your node is running correctly.

## 🧐 About This Project

This repository contains the necessary tools and information to run a validator node on the **Orbion testnet**. As a validator, you play a crucial role in securing the network by verifying transactions and creating new blocks. In return for your service, you are rewarded with coins.

This guide assumes you are starting with little to no experience in running a blockchain node.

-----

## 🛠️ What You'll Need (Prerequisites)

Before we begin, make sure you have these tools. If you don't, we've included links to help you install them.

1.  **A Command-Line Interface (CLI):**

      * **Windows:** **PowerShell** or **Command Prompt (CMD)**. Comes pre-installed.
      * **Mac:** **Terminal**. Comes pre-installed.
      * **Linux:** **Bash** or any other terminal. Comes pre-installed.
      * *This is the black window where you'll be typing all the commands.*

2.  **Git:** A tool for downloading code from repositories like GitHub.

      * *You can download it from [git-scm.com](https://git-scm.com/downloads).*

-----

## 📂 Understanding The Node Files

Inside the repository, you'll find a folder named `Node`. This folder contains the core executables:

  * `Node/geth.exe` (or `geth` on Linux/Mac): This is the **main program**, the engine of your node. It handles connecting to the network, downloading the blockchain, and mining.
  * `Node/bootnode.exe`: A small helper program that can assist nodes in finding each other on the network.
  * `Node/clef.exe`: An external tool for managing your accounts and signing transactions securely. This is an advanced feature not covered in this beginner's guide.

-----

## 🏁 Step-by-Step Setup Guide

Follow these steps in order.

### Step 1: Get the Node Files

First, you need to download all the necessary files from the repository onto your computer.

Open your terminal and run this command:

```bash
# This command downloads the project into a new folder named "Orbion-Node"
git clone https://github.com/orbionchain/Orbion-Node.git

# Now, navigate into that new folder
cd Orbion-Node
```

You are now in the project's main directory. All other commands should be run from here.

### Step 2: Create the Genesis File

Every blockchain starts with a "Block 0," known as the **Genesis Block**. This file, `genesis.json`, contains the configuration and rules for the entire blockchain.

Create a new file named `genesis.json` inside your `Orbion-Node` folder and put the exact content below into it.

```json
// --- PASTE THE CONTENT BELOW INTO YOUR genesis.json FILE ---
{
  "config": {
    "chainId": 109901,
    "homesteadBlock": 0,
    "eip150Block": 0,
    "eip155Block": 0,
    "eip158Block": 0,
    "byzantiumBlock": 0,
    "constantinopleBlock": 0,
    "petersburgBlock": 0,
    "istanbulBlock": 0,
    "berlinBlock": 0,
    "clique": {
      "period": 5,
      "epoch": 30000
    }
  },
  "difficulty": "1",
  "gasLimit": "8000000",
  "extradata": "0x0000000000000000000000000000000000000000000000000000000000000000c820447a576d87379f655e5518185e03457058f1675777af60c0411883a4c460f4ffcb1ea80e6a330000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
  "alloc": {
    "c820447a576d87379f655e5518185e03457058f1": {
      "balance": "100000000000000000000000000"
    },
    "675777af60C0411883A4C460F4fFCB1eA80e6A33": {
      "balance": "100000000000000000000000000"
    }
  }
}
```

### Step 3: Create Your Validator Wallet 🔑

You need a wallet address (also called an "account") to receive your validation rewards. Let's create one.

Run the following command. It will ask you for a password.
**Choose a strong password and save it somewhere safe\! If you lose it, you lose access to your wallet forever.**

  * **For Windows (PowerShell):**
    ```powershell
    .\Node\geth.exe --datadir ./data account new
    ```
  * **For Linux / macOS (Bash):**
    ```bash
    ./Node/geth --datadir ./data account new
    ```

After you enter and confirm your password, the command will output your new public address. It looks like this: `0x...`. **Copy this address and save it.** You will need it for the next steps.

### Step 4: Initialize the Blockchain

Now we need to prepare the node's database using the `genesis.json` file. This command only needs to be run **once**.

  * **For Windows (PowerShell):**
    ```powershell
    .\Node\geth.exe --datadir ./data init .\genesis.json
    ```
  * **For Linux / macOS (Bash):**
    ```bash
    ./Node/geth --datadir ./data init genesis.json
    ```

You should see a message like `Successfully wrote genesis state`.

### Step 5: Get Your Validator Approved ✅

**This is a critical step.** Before your node can successfully create blocks, your wallet address must be approved by a network administrator.

1.  **Join the official Telegram group:** [**CLICK HERE TO JOIN**](https://t.me/OrbionNetwork) \<-- *Ganti dengan link grup Telegram Anda*
2.  **Request Approval:** Send a message to the group or an admin. State that you would like to be a validator.
3.  **Provide Your Address:** When asked, provide the public wallet address you created in **Step 3**.

Wait for confirmation from the admin that your address has been added to the validator set. **Do not proceed to the next step until you are approved.**

### Step 6: Start Your Node and Connect\! 🌐

Once you are approved, you can start your node. The command is long, so let's review what each part does.

| Flag                | What it does                                                                  |
| ------------------- | ----------------------------------------------------------------------------- |
| `--datadir`         | Tells the node where its database is.                                         |
| `--networkid`       | The network ID, which is `109901` for Orbion.                                   |
| `--bootnodes`       | The address of the "matchmaker" node to find others.                          |
| `--http`            | Enables applications like MetaMask to talk to your node.                      |
| `--mine`            | **Tells your node to start validating (mining).** |
| `--miner.etherbase` | **Sets the wallet address where your rewards will be sent.** |

Now, assemble the command using the template below. **You must replace `<YOUR_WALLET_ADDRESS>` with the address you created in Step 3.**

  * **Final Command (Windows - PowerShell):**

    ```powershell
    .\Node\geth.exe --datadir ./data --networkid 109901 --bootnodes "enode://8dc9f4362a8fe37ce936674f3424fadb628b5a5a538f53e5e6c901cd5af2fd538b80c68b259fba221f13ad2b84c5300624aeace1cb40bc88273a00c0c54726a5@bootnode.orbionchain.com:30305" --syncmode "full" --http --http.addr "0.0.0.0" --http.port "8545" --http.corsdomain "*" --mine --miner.etherbase <YOUR_WALLET_ADDRESS>
    ```

  * **Final Command (Linux / macOS - Bash):**

    ```bash
    ./Node/geth --datadir ./data --networkid 109901 --bootnodes "enode://8dc9f4362a8fe37ce936674f3424fadb628b5a5a538f53e5e6c901cd5af2fd538b80c68b259fba221f13ad2b84c5300624aeace1cb40bc88273a00c0c54726a5@bootnode.orbionchain.com:30305" --syncmode "full" --http --http.addr "0.0.0.0" --http.port "8545" --http.corsdomain "*" --mine --miner.etherbase <YOUR_WALLET_ADDRESS>
    ```

Once you run this command, your node will start\! You will see a lot of log messages as it looks for peers and syncs the blockchain. If you are approved, you will eventually see messages about successfully sealing new blocks.

-----

## ✅ Checking Your Node's Status

To interact with your running node, open a **new, separate terminal window**. Then run the "attach" command:

  * **Windows:** `.\Node\geth.exe attach http://127.0.0.1:8545`
  * **Linux/Mac:** `./Node/geth attach http://127.0.0.1:8545`

This opens an interactive console. Here are some useful commands:

  * `eth.syncing`: If it returns `false`, your node is fully synced.
  * `net.peerCount`: Shows how many other nodes you are connected to. Should be greater than 0.
  * `eth.blockNumber`: Shows the current latest block number your node has.
  * `miner.getEtherbase()`: Should show the wallet address you are mining to.

-----

## ⚠️ Important Security Notice

  * **Firewall:** Your computer's firewall might block the node from connecting to others. You may need to allow incoming/outgoing connections for port `30303` (the default P2P port).
  * **Keys and Passwords:** Never share the files in your `data/keystore` directory or your password. They control your funds.

-----

## 📜 License

This software is distributed under the GNU General Public License v3.0. You can read the full license in the `COPYING` file.
