# Bitz Node Android 
An Easy Guide to Run Bitz Node in Android Using Termux/Userland.

**🩷Follow our TG for More Early Alpha: https://telegram.me/cryptomythx**
---

# First Install Termux or Userland

1. Termux: https://f-droid.org/packages/com.termux
2. Userland: https://play.google.com/store/apps/details?id=tech.ula **(Recommended)**

(Userland Is Easy Cause You No Need to Install Ubuntu Nanually, But Termux is Also Ok)

# If You're Using Userland

1. Install Application
2. Select Ubuntu
3. Select Minimal
4. Continue With SSH (We Don't Need GUI)
5. Allow to Download File
6. Wait Until Finished

# If You're Using Termux

Install Ubuntu in Termux:
```bash
pkg update && pkg upgrade
pkg install proot-distro
proot-distro install ubuntu-20.04
```

Login to Ubuntu:
```bash
proot-distro login ubuntu-20.04
```

After Installing Ubuntu Follow Below Steps 👇:

## Install Dependecies
**1. Install Packages**
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y build-essential clang cmake curl git libssl-dev pkg-config
```

**2. Install CA Certificates:**
```bash
sudo apt update
sudo apt install --reinstall ca-certificates
sudo update-ca-certificates
```

**2. Install Rust:**
```bash
 curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source $HOME/.cargo/env
rustup update
```
* When Prompted, Enter `1` and wait unti installation compelete.

  
**3. Clone Solana Repo:**
```bash
git clone https://github.com/solana-labs/solana.git
cd solana
```

**4. Build Solana CLI:**
```bash
cargo build --release
```
*Note: This process may take some time, especially on devices with limited resources. 

**5. Move Solana CLI to Ubuntu:**
```bash
sudo cp target/release/solana /usr/local/bin/
```

**6. Move Keygen:**
```bash
sudo cp target/release/solana-keygen /usr/local/bin/
```

**Exit From Termux/Userland (Close Session) and Reopen**
(If Using Termux Login Ubuntu, If Using Userland It Will Auto Login to Ubuntu)

**7. Check Solana Version:**
```bash
solana --version
```

**8. Switch RPC**
```bash
solana config set --url https://mainnetbeta-rpc.eclipse.xyz/
```

---

## CLI Wallet
### 1. Create a CLI wallet
```bash
solana-keygen new
```
---

## Install Bitz
```bash
cargo install bitz
```

---

## Run Bitz Miner
### 1. Open a screen

```bash
screen -S bitz
```

### 2. Start Miner
```bash
bitz collect
```

![image](https://github.com/user-attachments/assets/7c526a4b-07da-4ad5-889f-17674761b5e7)


### Usefull Commands

Check account info:
```bash
bitz account
```

To integrate Node & Backpack address

```bash
cat ~/.config/solana/id.json
```
(Copy Your Private Key From First [ to ] Including Brackets)

**Import Wallet in Backpack Wallet**
1. Open Backpack Wallet
2. Go to Import (Select Eclipse Network)
3. Select Private Key
4. Paste Private Key
5. Import

*Make Sure to Add atleast $1 Eclipse ETH in this Wallet to Be Able to Start Node & Claim Reward*

**Claim Bitz to your Node Wallet:**
```bash
bitz claim
```
*Claiming on Every 24H is Recommended*


# Important Tips
1. Make Sure Do Not Close Terminal
2. Keep in Background
3. Acquire Wake clock (Prevent Auto Stop)
4. Do Not Turn on Battery Saver
5. Give Permission to Run in Background (Termux/Userland)

# Auto Start Script
Now Let's Configure Auto Start Script, Because Bitz Node Sometimes Automatically Crash, Cause of Heavy Traffic in The Network. 

**1. Create Auto Script**
```bash
nano auto-bitz.sh
```

**2. Paste This Code**
```bash
#!/bin/bash

while true; do
    echo "Starting bitz node..."
    bitz collect
    echo "bitz crashed. Restarting in 5 seconds..."
    sleep 5
done
```

*After Pasting this Code Press Ctrl+x and y then hit Enter*


**3. Make it Executable**
```bash
chmod 777 auto-bitz.sh
```

**4. Start Screen**
```bash
screen -S bitz
```

**5. Run Auto Script**
```bash
./auto-bitz.sh
```

*Now This Script Will Restart Your Node Automatically After Crash, You Need to Manually Restart on Every Crash*
