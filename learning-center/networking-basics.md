# Networking - Basics

## 🌐 Networking Basics (for Servers)

When running a node or validator, understanding basic networking is **very important**. This helps you solve problems related to syncing, peer connections, RPC access, and firewalls.

This page covers:

* Public & Private IP
* Ports & Port Forwarding
* Basic tools for networking
* Common network troubleshooting

***

### 🌍 Public IP vs Private IP

* **Public IP**: The IP address visible to the internet. Your node uses this to communicate with other peers or to expose an RPC/API.
* **Private IP**: Local IP used inside a private network (like `192.168.x.x`). Useful for internal-only services.

> VPS servers usually get a **Public IP** by default. You can see it with:

```bash
curl ifconfig.me
```

### 🔢 What is a Port?

A **port** is like a door to your server. Each app/service runs on a different port.

Examples:

| Service    | Default Port |
| ---------- | ------------ |
| SSH        | 22           |
| HTTP       | 80           |
| HTTPS      | 443          |
| Cosmos P2P | 26656        |
| Cosmos RPC | 26657        |

***

### 🎯 Port Forwarding (NAT)

> **Relevant mostly for home servers or local VMs**, not typical VPS setups.

If you're running a node from your home or local network, your **router/firewall** might block outside connections.

You’ll need to:

1. Login to your router admin page
2. Go to **Port Forwarding / NAT** settings
3. Forward the needed port (e.g. 26656) to your local server IP

> For example: Forward `26656` to `192.168.1.100`

***

### 🚦 Allowing Ports in Ubuntu Firewall (UFW)

By default, Ubuntu might block certain ports. Use `ufw` to allow them:

```bash
# Enable UFW
sudo ufw enable

# Allow SSH (important to avoid locking yourself out!)
sudo ufw allow 22

# Allow Cosmos P2P & RPC ports
sudo ufw allow 26656
sudo ufw allow 26657

# Check status
sudo ufw status
```

***

### 🧪 Useful Networking Commands

#### 🔍 Check open ports on your server:

```bash
sudo lsof -i -P -n | grep LISTEN
```

#### 📡 Check public IP:

```bash
curl ifconfig.me
```

#### 🔗 Test if a port is open (from outside):

```bash
telnet <your-server-ip> 26656
```

#### 🧱 Check if a port is blocked by firewall:

```bash
nc -zv <your-server-ip> 26656
```

***

### 🔄 Connecting to Peers

Most blockchain nodes need to **connect to other peers**. Make sure:

* Your `p2p` port is open
* You're not behind NAT (or have port forwarding)
* You’re advertising your correct external IP in config (e.g. `external_address = "<ip>:<port>"`)

***

### 📊 Monitor Who's Connecting

```bash
sudo netstat -tulnp
```

Or using `ss`:

```bash
sudo ss -tuln
```

To see SSH login attempts:

```bash
journalctl -u ssh
```

***

### 🚫 Block Dangerous Traffic

Block unused ports and protocols. Example:

```bash
sudo ufw deny 8000
sudo ufw deny from 0.0.0.0/0 to any port 23 proto tcp
```

> Don’t expose unnecessary services like FTP, Telnet, or open databases.
