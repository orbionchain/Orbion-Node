````markdown
# Orbion Validator Node — Complete Setup Guide 🚀

Welcome!  
This guide will walk you through every step required to set up and run a validator node on the Orbion Testnet. No prior blockchain experience required. All instructions are clearly separated for Linux/macOS and Windows users. Let’s get started!

---

## 1. System Requirements

**Hardware Recommendations**
- **CPU:** 4+ cores (modern Intel/AMD or ARM)
- **RAM:** 8 GB or more
- **Disk:** SSD, at least 100 GB free space
- **Internet:** Reliable broadband, minimum 10 Mbps up/down

**Software Requirements**
- **Git** ([Download here](https://git-scm.com/downloads))
- **Terminal:**  
  - Linux/macOS: Terminal or Bash shell  
  - Windows: PowerShell (recommended) or CMD

---

## 2. Download the Orbion Node Repository

Open your terminal (or PowerShell) and run:

```bash
git clone https://github.com/orbionchain/Orbion-Node.git
cd Orbion-Node
````

---

## 3. Create a Validator Wallet

This wallet will receive your rewards.
**Write down your password and new wallet address. You will need them later!**

### Linux/macOS

```bash
./Node/geth --datadir ./data account new
```

### Windows (PowerShell)

```powershell
.\Node\geth.exe --datadir .\data account new
```

* Follow the prompts to enter and confirm your password.
* After creation, your new address will look like `0x1234...ABCD`.
* **Copy and save both the password and the address.**

---

## 4. Initialize the Blockchain Database

This step configures your local node to follow the Orbion testnet rules.
**Only run this step once per setup.**

### Linux/macOS

```bash
./Node/geth --datadir ./data init genesis.json
```

### Windows (PowerShell)

```powershell
.\Node\geth.exe --datadir .\data init .\genesis.json
```

You should see:
`Successfully wrote genesis state`

---

## 5. Get Validator Approval

Your wallet **must** be approved before your node can validate blocks.

1. **Join the Orbion Testnet Telegram:**
   [https://t.me/OrbionNetwork](https://t.me/OrbionNetwork)
2. **Request validator approval:**
   Send your wallet address (from Step 3) and request to be added as a validator.
3. **Wait for confirmation** from an admin.

---

## 6. Save Your Wallet Password

You’ll need to unlock your account for mining.

* In the `Orbion-Node` directory, create a text file named:

  * `password.txt`
* The file should contain **only your password** (no quotes, no spaces, no line breaks).

Example (password file content):

```
yourSuperSecretPassword
```

---

## 7. Start Your Node (Single Command)

**You must replace `<YOUR_WALLET_ADDRESS>` with your real address from Step 3.**

### Linux/macOS

```bash
./Node/geth --datadir ./data --networkid 109901 --bootnodes "enode://8dc9f4362a8fe37ce936674f3424fadb628b5a5a538f53e5e6c901cd5af2fd538b80c68b259fba221f13ad2b84c5300624aeace1cb40bc88273a00c0c54726a5@bootnode.orbionchain.com:30305" --port 30303 --http --http.addr "0.0.0.0" --http.port 8545 --http.api "eth,net,web3,personal,miner,txpool" --http.corsdomain "virtual-testnet.orbionchain.com" --http.vhosts "virtual-testnet.orbionchain.com" --allow-insecure-unlock --unlock "<YOUR_WALLET_ADDRESS>" --password ./password.txt --miner.etherbase <YOUR_WALLET_ADDRESS> --mine --verbosity 3 console
```

### Windows (PowerShell)

```powershell
.\Node\geth.exe --datadir .\data --networkid 109901 --bootnodes "enode://8dc9f4362a8fe37ce936674f3424fadb628b5a5a538f53e5e6c901cd5af2fd538b80c68b259fba221f13ad2b84c5300624aeace1cb40bc88273a00c0c54726a5@bootnode.orbionchain.com:30305" --port 30303 --http --http.addr "0.0.0.0" --http.port 8545 --http.api "eth,net,web3,personal,miner,txpool" --http.corsdomain "virtual-testnet.orbionchain.com" --http.vhosts "virtual-testnet.orbionchain.com" --allow-insecure-unlock --unlock "<YOUR_WALLET_ADDRESS>" --password "password.txt" --miner.etherbase <YOUR_WALLET_ADDRESS> --mine --verbosity 3 console
```

**Tip:**
You can close the node console with `CTRL+C` (the node will stop).

---

## 8. Run Your Node 24/7 (Background/Service Mode)

To keep your node running even when you close your terminal:

### Linux/macOS

```bash
nohup ./Node/geth --datadir ./data --networkid 109901 --bootnodes "enode://8dc9f4362a8fe37ce936674f3424fadb628b5a5a538f53e5e6c901cd5af2fd538b80c68b259fba221f13ad2b84c5300624aeace1cb40bc88273a00c0c54726a5@bootnode.orbionchain.com:30305" --port 30303 --http --http.addr "0.0.0.0" --http.port 8545 --http.api "eth,net,web3,personal,miner,txpool" --http.corsdomain "virtual-testnet.orbionchain.com" --http.vhosts "virtual-testnet.orbionchain.com" --allow-insecure-unlock --unlock "<YOUR_WALLET_ADDRESS>" --password ./password.txt --miner.etherbase <YOUR_WALLET_ADDRESS> --mine --verbosity 3 > orbion-node.log 2>&1 &
```

* To see logs: `tail -f orbion-node.log`
* To stop: `ps aux | grep geth` then `kill <PID>`

### Windows (PowerShell)

1. Open Notepad, paste the following (edit `<YOUR_WALLET_ADDRESS>`):

   ```powershell
   Start-Process -FilePath ".\Node\geth.exe" -ArgumentList "--datadir .\data --networkid 109901 --bootnodes 'enode://8dc9f4362a8fe37ce936674f3424fadb628b5a5a538f53e5e6c901cd5af2fd538b80c68b259fba221f13ad2b84c5300624aeace1cb40bc88273a00c0c54726a5@bootnode.orbionchain.com:30305' --port 30303 --http --http.addr '0.0.0.0' --http.port 8545 --http.api 'eth,net,web3,personal,miner,txpool' --http.corsdomain 'virtual-testnet.orbionchain.com' --http.vhosts 'virtual-testnet.orbionchain.com' --allow-insecure-unlock --unlock '<YOUR_WALLET_ADDRESS>' --password 'password.txt' --miner.etherbase <YOUR_WALLET_ADDRESS> --mine --verbosity 3" -NoNewWindow
   ```
2. Save as `start-node.ps1` in the `Orbion-Node` directory.
3. Start from PowerShell:

   ```powershell
   .\start-node.ps1
   ```
4. To stop: open Task Manager, find `geth.exe`, and End Task.

---

## 9. Checking Your Node Status

You can open a **second terminal window** to interact with your running node.

### Linux/macOS

```bash
./Node/geth attach http://127.0.0.1:8545
```

### Windows

```powershell
.\Node\geth.exe attach http://127.0.0.1:8545
```

Inside the Geth console, useful commands:

* `eth.syncing`
  Returns `false` when fully synced.
* `net.peerCount`
  Shows number of peers (should be > 0).
* `eth.blockNumber`
  Current block height.
* `miner.getEtherbase()`
  Shows the mining reward address.

---

## 10. Security Recommendations

* **Never share your `data/keystore` or `password.txt` file.** These control your funds!
* Make sure firewall allows TCP port `30303` for peer connectivity.
* Regularly back up your wallet address, password, and `genesis.json`.

---

## 11. Need Help?

If you have issues or questions, join the Orbion Testnet [Telegram group](https://t.me/OrbionNetwork) for help and community support.

---

## 12. License

This software is released under the GNU General Public License v3.0.
See the `COPYING` file in this repository for full license text.

