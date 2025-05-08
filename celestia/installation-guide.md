---
description: Celestia node installation guide
hidden: true
---

# Installation Guide

## Node Requirement

<table data-full-width="false"><thead><tr><th width="262.3333333333333">Requirement</th><th>Details</th></tr></thead><tbody><tr><td>CPU</td><td>4 Cores</td></tr><tr><td>RAM / Memory</td><td>8 GB</td></tr><tr><td>Storage</td><td>500 gb</td></tr><tr><td>Network</td><td>100 Mbps</td></tr><tr><td>OS</td><td>Ubuntu 22.0 (x64)</td></tr></tbody></table>

## Install dependencies

Included: Make, Go, Cosmovisor

```bash
# For the culture XD
sudo apt update && sudo apt upgrade -y

#make installaion
sudo apt install make

#removes any previous Go installation
sudo rm -rvf /usr/local/go/

#install Go
wget https://golang.org/dl/go1.22.3.linux-amd64.tar.gz
sudo tar -C /usr/local -xzf go1.21.1.linux-amd64.tar.gz
rm go1.21.1.linux-amd64.tar.gz

#Configure Go
export GOROOT=/usr/local/go
export GOPATH=$HOME/go
export GO111MODULE=on
export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin

#Install Cosmovisor
go install github.com/cosmos/cosmos-sdk/cosmovisor/cmd/cosmovisor@v1.0.0

```

> _\*if you have already, install dependencies_ necessary _only. /or update your dependencies to latest version if needed._



## 1. Install Node

Current Node version: **v1.9.0**

```bash
git clone https://github.com/celestiaorg/celestia-app celestia
cd celestia
git checkout v1.9.0 #Tips: check github & use LTS version
make install
```

## 2. Configure

### Initialize Node

Replace "MONIKER" with your own moniker and set chain-id. For example running on mainnet eg; celestia

```bash
celestia-appd init YOUR_MONIKER --chain-id celestia
```

**Network / chain-id info:**

**Mainnet:** <mark style="background-color:blue;">celestia</mark>

**Testnet:** <mark style="background-color:blue;">celestia-1</mark>

eg:

> ```
> celestia-appd init prolinkmoon --chain-id celestia-1 #Example for Testnet Node
> ```



### Download Genesis

The genesis file link below is Polkachu's mirror download. The best practice is to find the official genesis download link. \*but, Prolinkmoon will provide soon ..

```bash
wget -O genesis.json https://snapshots.polkachu.com/genesis/celestia/genesis.json --inet4-only
mv genesis.json ~/.celestia-app/config
```

### **Configure Seeds**

Using a seed node to bootstrap is the best practice in our view. Alternatively, you can use addrbook or persistent\_peers. \*use Polkachu Seeds, 'cause Prolinkmoon infra not 100% perfect for now.

```
sed -i 's/seeds = ""/seeds = "ade4d8bc8cbe014af6ebdf3cb7b1e9ad36f412c0@seeds.polkachu.com:11656"/' ~/.celestia-app/config/config.toml
```

\
**Snapshot (optional)**

use [Polkachu's provider](https://polkachu.com/tendermint_snapshots/celestia), because Prolinkmoon doesn't provide it at this time.&#x20;

## 3. Launch Node

### **Configure Cosmovisor Folder**

Create Cosmovisor folders and load the node binary.

```bash
# Create Cosmovisor Folders
mkdir -p ~/.celestia-app/cosmovisor/genesis/bin
mkdir -p ~/.celestia-app/cosmovisor/upgrades

# Load Node Binary into Cosmovisor Folder
cp ~/go/bin/celestia-appd ~/.celestia-app/cosmovisor/genesis/bin
```

### **Create Service File**

Create a `celestia.service` file in the `/etc/systemd/system` folder with the following code snippet. Make sure to replace `USER` with your Linux user name. You need sudo privilege to do this step.

```
[Unit]
Description="celestia node"
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

### **Start Node Service**

```
# Enable service
sudo systemctl enable celestia.service

# Start service
sudo service celestia start

# Check logs
sudo journalctl -fu celestia
```

\
