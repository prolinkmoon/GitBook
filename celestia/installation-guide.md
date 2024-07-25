---
description: Celestia node installation guide
---

# Installation Guide

## Node Requirement

<table data-full-width="false"><thead><tr><th width="262.3333333333333">Requirement</th><th>Details</th></tr></thead><tbody><tr><td>CPU</td><td>4 Cores</td></tr><tr><td>RAM / Memory</td><td>8 GB</td></tr><tr><td>Storage</td><td>500 gb</td></tr><tr><td>Network</td><td>100 Mbps</td></tr><tr><td>OS</td><td>Ubuntu 22.0 (x64)</td></tr></tbody></table>

## Install dependencies

Included: Make, Go, Cosmovisor

```sh
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
git checkout v1.9.0
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

### Download Genesis

### **Configure Seeds**

\
**Snapshot (optional)**

