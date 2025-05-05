# Docker - Basics

## 🐳 Docker – Basics

Docker is a tool that makes it easy to run applications in isolated environments called **containers**. It’s lightweight, fast, and very useful when dealing with blockchain nodes, APIs, or backend tools.

***

### 🧠 What is Docker (In Simple Words)?

Think of Docker like a box.

* You put an app and everything it needs inside this box.
* You can send this box to any server.
* It will run exactly the same way everywhere.

This is helpful because:

* You don’t have to install dependencies manually.
* It avoids "works on my machine" problems.
* It saves time when setting up or migrating.

***

### 🧰 Why Use Docker in Crypto?

In the crypto world, Docker is commonly used to:

* Run blockchain nodes (e.g. Ethereum, Cosmos, Aptos)
* Host explorers, RPC servers, or tooling
* Build reproducible environments for testnets

***

### ⚙️ How to Install Docker on Ubuntu (VPS)

**For Ubuntu 20.04 or 22.04**, run the following steps:

```bash
# Update package list
sudo apt update

# Install Docker dependencies
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common

# Add Docker’s official GPG key
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/docker.gpg

# Add Docker repo to APT sources
echo "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list

# Update package list again
sudo apt update

# Install Docker CE
sudo apt install -y docker-ce

# Enable Docker to start at boot
sudo systemctl enable docker
sudo systemctl start docker

# Check Docker version
docker --version
```

> ✅ Done! Docker is now installed and ready to use.

Optional: Add your user to the Docker group (to run docker without `sudo`):

```bash
sudo usermod -aG docker $USER
```

Then log out and log back in, or run `newgrp docker`.

***

### 📦 Example: Running a Simple Container

Let’s try running an Ubuntu container:

<pre class="language-bash"><code class="lang-bash"><strong>docker run -it ubuntu
</strong></code></pre>

This will:

* Download the Ubuntu image (if not already downloaded)
* Start an interactive shell inside the container

You can now run Linux commands inside this isolated environment.

To exit: just type `exit`

***

### 🧪 Example: Running a Blockchain Node with Docker

Here’s an example for running a Cosmos SDK chain node (e.g. Gaia):

```bash
docker run -it ghcr.io/cosmos/gaia:v23.2.0 gaiad version
```

You can also run full nodes with volume mounting and config, like:

```bash
docker run -d \
  --name gaiad-node \
  -v $HOME/.gaia:/root/.gaia \
  -p 26656:26656 \
  -p 26657:26657 \
  ghcr.io/cosmos/gaia:v23.2.0 \
  gaiad start
```

This will:

* Run the node in background (`-d`)
* Mount your config directory
* Expose the necessary ports

***

### 🗑️ Cleaning Up Docker

To see running containers:

```bash
docker ps
```

To stop a container:

```bash
docker stop <container-id>
```

To remove a container:

```bash
docker rm <container-id>
```

To list all images:

```bash
docker images
```

To remove an image:

```bash
docker rmi <image-id>
```

***

### 🧠 Summary

| Term       | Meaning                                      |
| ---------- | -------------------------------------------- |
| Container  | A lightweight, isolated instance of an app   |
| Image      | The package used to create a container       |
| Volume     | A shared folder between your host and Docker |
| Docker Hub | Public repo of Docker images                 |

***

💡 _Docker is a must-have tool for DevOps and node runners. Once you get used to it, it’ll save you hours of setup time._

Next → Learn how to **run your validator in Docker** or **monitor logs inside containers**.
