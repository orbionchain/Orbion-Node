# Orbion Node Validator: A Complete Guide for Beginners 🚀

Welcome\! This guide is designed to walk you through the process of setting up an **Orbion Validator Node** from scratch. We'll explain every step, what each command does, and how to ensure your node is running correctly.

## 🧐 About This Project

This repository contains the necessary tools and information to run a validator node on the **Orbion testnet**. As a validator, you play a crucial role in securing the network by verifying transactions and creating new blocks. In return for your service, you are rewarded with coins.

This guide assumes you are starting with little to no experience in running a blockchain node.

-----

## 🛠️ What You'll Need (Prerequisites)

Before we begin, make sure you have these tools.

1.  **A Command-Line Interface (CLI):**
      * **Windows:** **PowerShell** or **CMD**.
      * **Mac/Linux:** **Terminal** or **Bash**.
2.  **Git:** A tool for downloading code from repositories like GitHub.
      * *You can download it from [git-scm.com](https://git-scm.com/downloads).*

-----

## 📂 Understanding The Project Files

Inside the repository, you'll find these important items:

  * `Node/` (folder): Contains the core programs like `geth.exe`, the engine of your node.
  * `genesis.json` (file): This is the "founding document" or the "Big Bang" of the blockchain. It defines the network's core rules and initial state.
  * `COPYING` (file): The software license.

-----

## 🏁 Step-by-Step Setup Guide

Follow these steps in order.

### Step 1: Get the Project Files

First, download all the necessary files from the repository onto your computer using Git.

Open your terminal and run this command:

```bash
# This command downloads the project into a new folder named "Orbion-Node"
git clone https://github.com/orbionchain/Orbion-Node.git

# Now, navigate into that new folder
cd Orbion-Node
```

You are now in the project's main directory. All other commands should be run from here.

### Step 2: Create Your Validator Wallet 🔑

You need a wallet address (account) to receive your validation rewards. Let's create one.

Run the following command. It will ask you for a password. **Choose a strong password and save it somewhere safe\! If you lose it, you lose access to your wallet forever.**

  * **For Windows (PowerShell):**
    ```powershell
    .\Node\geth.exe --datadir ./data account new
    ```
  * **For Linux / macOS (Bash):**
    ```bash
    ./Node/geth --datadir ./data account new
    ```

After you enter and confirm your password, the command will output your new public address. It looks like this: `0x...`. **Copy this address and save it.** You will need it for the next steps.

### Step 3: Initialize the Blockchain

Now we need to prepare the node's database using the `genesis.json` file. This command reads the genesis file and sets up your data directory according to the network's rules.

This `init` command only needs to be run **once**.

  * **For Windows (PowerShell):**
    ```powershell
    .\Node\geth.exe --datadir ./data init .\genesis.json
    ```
  * **For Linux / macOS (Bash):**
    ```bash
    ./Node/geth --datadir ./data init genesis.json
    ```

You should see a message like `Successfully wrote genesis state`.

### Step 4: Get Your Validator Approved ✅

**This is a critical step.** Before your node can successfully create blocks, your wallet address must be approved by a network administrator.

1.  **Join the official Telegram group:** [**CLICK HERE TO JOIN**](https://t.me/OrbionNetwork)
2.  **Request Approval:** Send a message to the group or an admin. State that you would like to be a validator.
3.  **Provide Your Address:** When asked, provide the public wallet address you created in **Step 2**.

Wait for confirmation from the admin that your address has been added to the validator set. **Do not proceed to the next step until you are approved.**

### Step 5: Start Your Node and Connect\! 🌐

Once you are approved, you can start your node. To allow the node to automatically sign blocks, you first need to provide its password securely.

#### 5a. Create a Password File

To avoid typing your password every time, you'll save it in a file.

1.  In your `Orbion-Node` folder, create a new text file named `password.txt`.
2.  Inside this file, type **only your wallet password** and nothing else.
3.  Save and close the file.

#### 5b. Run the Node with Unlocked Account

Now, run the final command. We've added two new flags: `--unlock` to specify which account to use for validating, and `--password` to point to your new password file.

**You must replace `<YOUR_WALLET_ADDRESS>` with the address you created in Step 2.**

  * **Final Command (Windows - PowerShell):**

    ```powershell
    .\Node\geth.exe --datadir ./data --networkid 109901 --bootnodes "enode://8dc9f4362a8fe37ce936674f3424fadb628b5a5a538f53e5e6c901cd5af2fd538b80c68b259fba221f13ad2b84c5300624aeace1cb40bc88273a00c0c54726a5@bootnode.orbionchain.com:30305" --syncmode "full" --http --http.addr "0.0.0.0" --http.port "8545" --http.corsdomain "*" --mine --miner.etherbase <YOUR_WALLET_ADDRESS> --unlock <YOUR_WALLET_ADDRESS> --password "password.txt"
    ```

  * **Final Command (Linux / macOS - Bash):**

    ```bash
    ./Node/geth --datadir ./data --networkid 109901 --bootnodes "enode://8dc9f4362a8fe37ce936674f3424fadb628b5a5a538f53e5e6c901cd5af2fd538b80c68b259fba221f13ad2b84c5300624aeace1cb40bc88273a00c0c54726a5@bootnode.orbionchain.com:30305" --syncmode "full" --http --http.addr "0.0.0.0" --http.port "8545" --http.corsdomain "*" --mine --miner.etherbase <YOUR_WALLET_ADDRESS> --unlock <YOUR_WALLET_ADDRESS> --password "password.txt"
    ```

Now, your node will start, automatically unlock your account, and begin sealing new blocks successfully.

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
  * **Keys and Passwords:** Never share the files in your `data/keystore` directory or your `password.txt` file. They control your funds.

-----

## 📜 License

This software is distributed under the GNU General Public License v3.0. You can read the full license in the `COPYING` file.
