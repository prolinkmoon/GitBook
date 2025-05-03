---
description: '- a little guide to make it easier to understand'
---

# Book of node (Beginners)

## 🌐 Understanding Servers & Infrastructure (For Beginners)

Before we run a validator or node, we need to understand the basic tools and systems we’ll be using. Many new people in crypto DevOps come from non-technical backgrounds, so don’t worry — this section explains everything simply.

***

### 🖥️ What is a Server?

A **server** is just a computer that runs 24/7 and is usually placed in a data center. It’s not much different from your laptop, but it’s designed to stay online and be accessed remotely.

***

### ☁️ What is a VPS?

A **VPS (Virtual Private Server)** is a "virtual machine" — like a slice of a big server. You get your own space with Linux installed, but the physical hardware is shared with others.

Popular VPS providers:

* Contabo
* DigitalOcean
* Vultr
* Hetzner

More advanced providers:

* AWS (Amazon Web Services)
* Google Cloud
* Azure

***

### 🧱 Dedicated Server vs Bare Metal

* A **dedicated server** gives you full access to one physical machine.
* **Bare metal** usually means raw hardware with no virtualization — very high performance.

These are more expensive but used for high-stakes validators or mainnet operations.

***

### 📟 What is SSH?

**SSH (Secure Shell)** lets you connect to your remote server securely from your local computer.

Think of SSH like opening a terminal into your server from anywhere in the world.

Basic SSH command:

```bash
ssh username@your-server-ip
```

### 🌍 Public IP vs Private IP

* **Public IP** = The address the world sees. You use this to connect to your server from the internet.
* **Private IP** = Used inside data centers or internal networks (not accessible from outside).

For node setups, we usually use the **public IP**.

***

### 🐧 What is Ubuntu?

**Ubuntu** is a type of Linux — an open-source operating system that runs on most servers.

When people say "Linux server", they usually mean Ubuntu or Debian. Most crypto nodes use Ubuntu 20.04 or 22.04.

***

### ☁️ Choosing the Right Server Provider

Not all server providers are the same. Some are cheap but slow. Others are fast but expensive. It all depends on your needs — are you just testing, or running a serious mainnet validator?

Let’s break it down simply.

***

### 🔍 Types of Use Cases

| Use Case            | What You Need                              |
| ------------------- | ------------------------------------------ |
| Learning & Practice | Cheap VPS, small specs, monthly billing    |
| Testnet Validator   | Reliable VPS, enough CPU & RAM             |
| Mainnet Validator   | High performance (Dedicated or Bare Metal) |
| Archive or RPC Node | Large storage, fast network, high IOPS     |

***

### ⚖️ Comparing Popular Server Providers

| Provider     | Type             | Pricing       | Performance | Ease of Use | Best For                 |
| ------------ | ---------------- | ------------- | ----------- | ----------- | ------------------------ |
| Contabo      | VPS / Dedicated  | 💰 Cheap      | Medium      | ⭐⭐          | Testnets, backups        |
| Hetzner      | VPS / Bare Metal | 💵 Affordable | High        | ⭐⭐⭐         | Testnets & Mainnet       |
| Vultr        | VPS              | 💵 Medium     | Good        | ⭐⭐⭐⭐        | Simple testnet setups    |
| DigitalOcean | VPS              | 💵 Medium     | Good        | ⭐⭐⭐⭐        | Beginners                |
| AWS          | Cloud (VPS)      | 💸 Expensive  | Excellent   | ⭐⭐⭐⭐        | Mainnet + serious uptime |
| Google Cloud | Cloud (VPS)      | 💸 Expensive  | Excellent   | ⭐⭐⭐⭐        | Advanced use cases       |
| OVHcloud     | VPS / Dedicated  | 💵 Medium     | Good        | ⭐⭐          | Geo diversity, mainnets  |

***

### ✅ Cheap Doesn’t Mean Bad

Cheap providers like **Contabo** or **Hetzner** are great for testnets. They give you good specs for the price. But:

* Sometimes slower disk or network speed
* Support may be limited
* Downtime can happen (but rarely)

Still — great value for learning or experimenting.

***

### ⚡ When to Use Premium Providers

Use **AWS**, **Google Cloud**, or **DigitalOcean** if you need:

* Very high uptime
* Good global latency
* Advanced features (like backups, snapshots, API, autoscaling)

Downside? 💸 It’s expensive. Example: $80–200/month for specs that cost $10–30/month on Contabo or Hetzner.

***

### 🔧 Example Specs for Crypto Use

| Purpose            | CPU     | RAM    | Storage         | Provider Suggestion   |
| ------------------ | ------- | ------ | --------------- | --------------------- |
| Testnet Node       | 2 vCPU  | 4–8 GB | 100 GB SSD      | Contabo VPS / Hetzner |
| Mainnet Validator  | 4+ vCPU | 16+ GB | 500 GB NVMe     | Hetzner Bare Metal    |
| Archive / RPC Node | 8+ vCPU | 32+ GB | 2–4 TB NVMe SSD | AWS / Hetzner / OVH   |

***

### 🌍 Location Matters

Try to pick server locations close to your target chain’s region or other validators (Europe is usually safest).

Example:

* Cosmos chains: Frankfurt (EU), Helsinki
* Ethereum L2: US West or Central
* Sui, Aptos, etc.: Pick what the community uses (usually in docs or Discord)

***

### 🧠 Final Tips

* Start small, then upgrade if needed
* Always check for bandwidth limits (some providers have caps)
* Avoid trialing on AWS unless you’re okay with surprise bills 💥

***

📌 _For most beginners, we recommend starting with Contabo or Hetzner for the best balance of price and power._

### 🧠 Summary for Beginners

| Term             | Meaning                                                     |
| ---------------- | ----------------------------------------------------------- |
| VPS              | A virtual server (shared machine)                           |
| Dedicated Server | Full physical server (not shared)                           |
| Bare Metal       | Raw physical hardware                                       |
| Public IP        | The IP used to access your server from the internet         |
| Private IP       | Used internally inside a data center                        |
| SSH              | Secure way to access your server remotely                   |
| Ubuntu           | Popular Linux OS for running servers and crypto nodes       |
| Server Provider  | Company where you rent a VPS or server (AWS, Contabo, etc.) |
