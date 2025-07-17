# Orbion Node Validator: A Complete Guide for Beginners 🚀

Welcome\! This guide is designed to walk you through the process of setting up an **Orbion Validator Node** from scratch. We'll explain every step, what each command does, and how to ensure your node is running correctly.

## 🧐 About This Project

This repository contains the necessary tools and information to run a validator node on the **Orbion testnet**. As a validator, you play a crucial role in securing the network by verifying transactions and creating new blocks. In return for your service, you are rewarded with coins.

This guide assumes you are starting with little to no experience in running a blockchain node.

-----

## 🛠️ System and Software Requirements

Before we begin, ensure your system meets the following requirements.

### Hardware Specifications (Recommended)

To run a stable validator node, we recommend the following hardware specifications:

  * **CPU:** Modern processor with 4 or more cores.
  * **RAM:** 8 GB or more.
  * **Storage:** A Solid State Drive (SSD) with at least 100 GB of free space is highly recommended for better performance.
  * **Network:** A stable, high-speed internet connection (at least 10 Mbps).

### Software Prerequisites

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

Now, run the final command. This is the complete command with all necessary flags for a secure and stable validator node.

**You must replace `<YOUR_WALLET_ADDRESS>` with the address you created in Step 2.**

  * **Final Command (Windows - PowerShell):**

    ```powershell
    .\Node\geth.exe --datadir ./data --networkid 109901 --bootnodes "enode://8dc9f4362a8fe37ce936674f3424fadb628b5a5a538f53e5e6c901cd5af2fd538b80c68b259fba221f13ad2b84c5300624aeace1cb40bc88273a00c0c54726a5@bootnode.orbionchain.com:30305" --port 30303 --http --http.addr "0.0.0.0" --http.port 8545 --http.api "eth,net,web3,personal,miner" --http.corsdomain "virtual-testnet.orbionchain.com" --http.vhosts "virtual-testnet.orbionchain.com" --allow-insecure-unlock --unlock <YOUR_WALLET_ADDRESS> --password "password.txt" --mine --miner.etherbase <YOUR_WALLET_ADDRESS> --verbosity 3
    ```

  * **Final Command (Linux / macOS - Bash):**

    ```bash
    ./Node/geth --datadir ./data --networkid 109901 --bootnodes "enode://8dc9f4362a8fe37ce936674f3424fadb628b5a5a538f53e5e6c901cd5af2fd538b80c68b259fba221f13ad2b84c5300624aeace1cb40bc88273a00c0c54726a5@bootnode.orbionchain.com:30305" --port 30303 --http --http.addr "0.0.0.0" --http.port 8545 --http.api "eth,net,web3,personal,miner" --http.corsdomain "virtual-testnet.orbionchain.com" --http.vhosts "virtual-testnet.orbionchain.com" --allow-insecure-unlock --unlock <YOUR_WALLET_ADDRESS> --password "password.txt" --mine --miner.etherbase <YOUR_WALLET_ADDRESS> --verbosity 3
    ```

#### Configuration Breakdown

| Flag | Description |
| :--- | :--- |
| `--port 30303` | Sets the network port for peer-to-peer communication. |
| `--http.api "..."` | Defines which modules are accessible over HTTP (e.g., `eth`, `net`). |
| `--http.corsdomain "..."` | A security measure that only allows specified domains to make requests. |
| `--http.vhosts "..."` | Only allows connections that specify this host. Use your domain or IP address. |
| `--verbosity 3` | Sets the log detail level. 3 is standard (Info), 4 is for debugging. |
| `--allow-insecure-unlock`| Required to unlock an account when the HTTP server is running. |

-----

## 🚀 Running Your Node 24/7 (Advanced)

To be a reliable validator, your node must run continuously. If you close the terminal window, the node will stop. Here’s how to run it as a background process.

### For Linux / macOS (using `nohup`)

The `nohup` command (no hang-up) ensures the process keeps running, and `&` sends it to the background.

1.  **Navigate** to your `Orbion-Node` directory.

2.  **Run** the following command (replace the placeholder):

    ```bash
    nohup ./Node/geth --datadir ./data --networkid 109901 --bootnodes "enode://8dc9f4362a8fe37ce936674f3424fadb628b5a5a538f53e5e6c901cd5af2fd538b80c68b259fba221f13ad2b84c5300624aeace1cb40bc88273a00c0c54726a5@bootnode.orbionchain.com:30305" --port 30303 --http --http.addr "0.0.0.0" --http.port 8545 --http.api "eth,net,web3,personal,miner" --http.corsdomain "virtual-testnet.orbionchain.com" --http.vhosts "virtual-testnet.orbionchain.com" --allow-insecure-unlock --unlock <YOUR_WALLET_ADDRESS> --password "password.txt" --mine --miner.etherbase <YOUR_WALLET_ADDRESS> --verbosity 3 > orbion-node.log 2>&1 &
    ```

<!-- end list -->

  * Your node is now running in the background.
  * You can view the logs in real-time by running `tail -f orbion-node.log`.
  * To stop the node, find its process ID (`ps aux | grep geth`) and use the `kill` command.

### For Windows (using PowerShell `Start-Process`)

We can use `Start-Process` to run the node in a new, hidden window.

1.  **Open PowerShell** in your `Orbion-Node` directory.

2.  **Create a script file.** Make a new file named `start-node.ps1`.

3.  **Copy and paste** the following command into `start-node.ps1` (replace the placeholder):

    ```powershell
    Start-Process -FilePath ".\Node\geth.exe" -ArgumentList "--datadir ./data --networkid 109901 --bootnodes 'enode://8dc9f4362a8fe37ce936674f3424fadb628b5a5a538f53e5e6c901cd5af2fd538b80c68b259fba221f13ad2b84c5300624aeace1cb40bc88273a00c0c54726a5@bootnode.orbionchain.com:30305' --port 30303 --http --http.addr '0.0.0.0' --http.port 8545 --http.api 'eth,net,web3,personal,miner' --http.corsdomain 'virtual-testnet.orbionchain.com' --http.vhosts 'virtual-testnet.orbionchain.com' --allow-insecure-unlock --unlock <YOUR_WALLET_ADDRESS> --password 'password.txt' --mine --miner.etherbase <YOUR_WALLET_ADDRESS> --verbosity 3" -NoNewWindow
    ```

4.  **Save the file.**

5.  **Run the script** from your PowerShell terminal:

    ```powershell
    .\start-node.ps1
    ```

<!-- end list -->

  * Your node is now running in the background.
  * To stop it, open Task Manager, find the `geth.exe` process, and end it.

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

  * **Firewall:** Your computer's firewall might block the node from connecting to others. You may need to allow incoming/outgoing connections for port `30303`.
  * **Keys and Passwords:** Never share the files in your `data/keystore` directory or your `password.txt` file. They control your funds.

-----

## 📜 License

This software is distributed under the GNU General Public License v3.0. You can read the full license in the `COPYING` file.
