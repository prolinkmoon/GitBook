# Installation Guide

## 🪐 Celestia Node Setup Guide

A simplified and clean step-by-step guide for setting up a Celestia node (Testnet or Mainnet) using **Ubuntu Linux**. This guide includes installing dependencies, setting up the node, configuring Cosmovisor, and managing the service.

***

### 🧰 Node Requirements & Dependencies

We'll install essential tools and dependencies like `make`, `Go`, and `Cosmovisor`.

```bash
# Update & Upgrade Packages
sudo apt update && sudo apt upgrade -y

# Install build tools
sudo apt install make -y

# Remove any old Go installation
sudo rm -rf /usr/local/go

# Install Go (update if newer version available)
wget https://golang.org/dl/go1.22.3.linux-amd64.tar.gz
sudo tar -C /usr/local -xzf go1.22.3.linux-amd64.tar.gz
rm go1.22.3.linux-amd64.tar.gz

# Configure Go Environment
echo "export GOROOT=/usr/local/go" >> ~/.bashrc
echo "export GOPATH=\u$HOME/go" >> ~/.bashrc
echo "export GO111MODULE=on" >> ~/.bashrc
echo "export PATH=\$PATH:/usr/local/go/bin:\$HOME/go/bin" >> ~/.bashrc
source ~/.bashrc

# Install Cosmovisor
go install github.com/cosmos/cosmos-sdk/cosmovisor/cmd/cosmovisor@v1.0.0
```

> If Go or Cosmovisor is already installed, make sure it’s up to date.

***

### 🛠️ Install the Celestia Node

```bash
git clone https://github.com/celestiaorg/celestia-app
cd celestia-app
git checkout v1.9.0    # You can check GitHub for latest stable version
make install
```

***

### ⚙️ Node Initialization

Replace `YOUR_MONIKER` with a name for your node.

```bash
# For mainnet:
celestia-appd init YOUR_MONIKER --chain-id celestia

# For testnet:
celestia-appd init YOUR_MONIKER --chain-id celestia-1
```

***

### 🌱 Download Genesis File

Official genesis links are recommended. Example using Polkachu’s mirror:

```bash
wget -O genesis.json https://snapshots.polkachu.com/genesis/celestia/genesis.json --inet4-only
mv genesis.json ~/.celestia-app/config/genesis.json
```

***

### 🌐 Configure Seed Nodes

Use trusted seed nodes for better peer discovery:

```bash
sed -i 's/seeds = \"\"/seeds = \"ade4d8bc8cbe014af6ebdf3cb7b1e9ad36f412c0@seeds.polkachu.com:11656\"/' ~/.celestia-app/config/config.toml
```

***

### 📦 (Optional) Use Snapshot to Sync Faster

You can use snapshot services like [Polkachu](https://polkachu.com/tendermint_snapshots/celestia) for faster syncing. Be sure to follow up-to-date snapshot instructions from the provider.

***

### 🚀 Setup Cosmovisor

```
# Create Cosmovisor Folder Structure
mkdir -p ~/.celestia-app/cosmovisor/genesis/bin
mkdir -p ~/.celestia-app/cosmovisor/upgrades

# Move Binary into Cosmovisor Folder
cp ~/go/bin/celestia-appd ~/.celestia-app/cosmovisor/genesis/bin
```

***

### 🛎️ Create systemd Service File

Create the service file to run the node in the background:

```
sudo nano /etc/systemd/system/celestia.service
```

Paste this (replace `USER` with your actual Linux username):

```
[Unit]
Description=Celestia Node
After=network-online.target

[Service]
User=USER
ExecStart=/home/USER/go/bin/cosmovisor start
Restart=always
RestartSec=3
LimitNOFILE=4096
Environment="DAEMON_NAME=celestia-appd"
Environment="DAEMON_HOME=/home/USER/.celestia-app"
Environment="DAEMON_ALLOW_DOWNLOAD_BINARIES=false"
Environment="DAEMON_RESTART_AFTER_UPGRADE=true"
Environment="UNSAFE_SKIP_BACKUP=true"

[Install]
WantedBy=multi-user.target
```

Enable and start the service:

```
sudo systemctl enable celestia
sudo systemctl start celestia

# View Logs
sudo journalctl -fu celestia
```

***

✅ Done! Your Celestia node should now be running.
