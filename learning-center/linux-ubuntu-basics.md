---
description: some frequently used commands and tools
---

# Linux/Ubuntu - Basics

## 🐧 Linux Ubuntu Basics&#x20;

If you're new to Linux, this page is your starting point. Here are essential commands you'll use often while managing a node or validator server (VPS) on Ubuntu.

#### 🧭 Navigation

```bash
pwd                      # Show current working directory
ls                       # List files and folders
ls -l                    # Long listing (with permissions, size, date)
ls -a                    # Show hidden files (starting with .)
cd folder-name           # Change into a folder
cd ..                    # Go up one level
cd ~                     # Go to home directory
cd /path/to/folder       # Go to specific path
```

#### 🗃 Creating, Moving, Deleting Files & Folders

```bash
mkdir folder-name             # Create a folder
mkdir -p folder/subfolder     # Create nested folders

touch file.txt                # Create an empty file
cp file1.txt file2.txt        # Copy a file
mv oldname.txt newname.txt    # Rename or move a file
rm file.txt                   # Delete a file
rm -r folder-name             # Delete a folder and its contents
```

#### 📝 Viewing & Editing Files

```bash
cat file.txt                  # Show file content
nano file.txt                 # Open and edit a file
less file.txt                 # Scroll through long files (q to quit)
head file.txt                 # Show the first 10 lines
tail file.txt                 # Show the last 10 lines
tail -f file.txt              # View log output in real-time
```

#### 🔍 Searching and Finding

```bash
grep "word" file.txt          # Search for a word in a file
find . -name "*.log"          # Find all .log files in current folder
which binary-name             # Find location of a program
```

#### 🧰 System & Package Management

```bash
sudo apt update               # Update available packages
sudo apt upgrade              # Upgrade installed packages
sudo apt install packagename  # Install a new package
sudo apt remove packagename   # Remove a package
sudo apt autoremove           # Remove unused packages
```

#### 🔐 Permissions and Executables

```bash
chmod +x file.sh              # Make a file executable
chmod 755 script.sh           # Set specific permissions
chown user:group file         # Change file ownership
```

#### 🔁 Process & System Monitoring

```bash
top                          # View running processes
htop                         # Better version of top (install with apt)
ps aux | grep binary         # Find running process
kill PID                     # Stop a process by PID
df -h                        # Show disk usage
free -m                      # Show memory usage
uptime                       # Show system load and uptime
```

#### 📦 Archive & Compression

```bash
tar -xvf file.tar            # Extract .tar files
tar -xzvf file.tar.gz        # Extract .tar.gz files
tar -xvJf file.tar.xz        # Extract .tar.xz files
unzip file.zip               # Extract .zip files
```

#### 📡 Network Commands

<pre class="language-bash"><code class="lang-bash">curl ifconfig.me             # Show public IP
<strong>ping google.com              # Check network connection
</strong>netstat -tuln                # List listening ports (install: net-tools)
ss -tuln                     # Modern alternative to netstat
lsof -i :26656               # Check what's using port 26656
</code></pre>

#### 🎬Running in the Background with screen

| Task            | Command                      |
| --------------- | ---------------------------- |
| Install screen  | `sudo apt install screen -y` |
| Start screen    | `screen -S nodename`         |
| Detach screen   | `Ctrl + A` then `D`          |
| Reattach screen | `screen -r nodename`         |
| List sessions   | `screen -ls`                 |
| Kill session    | `screen -X -S name quit`     |

#### 🧹 Useful Shortcuts

```bash
!!                           # Repeat last command
!apt                         # Run last command starting with 'apt'
history                      # Show command history
clear                        # Clear the terminal screen
Ctrl + C                     # Stop a running command
Ctrl + D                     # Logout or close terminal session
Tab                          # Autocomplete file/folder names
```

***

## 🔐 Security Basics

Running a node means your server is connected to the internet 24/7. That also means it's open to attacks if you're not careful.

In this section, we'll go through basic but important steps to protect your VPS or bare-metal server. These are simple things that every node operator should do.

***

#### 1. Use a Strong Password or SSH Key🔑&#x20;

Avoid using weak passwords. The best way to connect to your server is with an **SSH key**, not a password.

To generate a key (on your local machine):

```bash
ssh-keygen -t rsa -b 4096
```

Then copy it to your server:

<pre class="language-bash"><code class="lang-bash"><strong>ssh-copy-id user@your-server-ip
</strong></code></pre>

Disable password login:

```bash
sudo nano /etc/ssh/sshd_config
```

Change or make sure these lines are set:

```nginx
PasswordAuthentication no
PermitRootLogin no
```

Then restart SSH:

```bash
sudo systemctl restart ssh
```

***

#### 2. Set Up a Basic Firewall (UFW) 🛡️&#x20;

Allow only the ports you need:

```bash
sudo apt install ufw -y
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow ssh
sudo ufw allow 26656         # Example: P2P port for Cosmos-based chains
sudo ufw allow 26657         # Example: RPC port (optional or restrict)
sudo ufw enable
```

You can check status:

```bash
sudo ufw status
```

***

#### 3. Fail2Ban – Protect SSH from Brute Force 🚫

```bash
sudo apt install fail2ban -y
```

This helps block IPs that try to brute-force into your server.

***

#### 4. Remove Unused Packages🧼

Keep your system clean:

```bash
sudo apt autoremove -y
```

***

#### 5. Keep the System Updated🛠️

Regular updates help fix known security issues:

```bash
sudo apt update && sudo apt upgrade -y
```

***

#### 6. Optional: Monitor Login Activity📋

Check who logged in and when:

```bash
last
```

Check failed login attempts:

```bash
sudo cat /var/log/auth.log | grep "Failed"
```

***

#### 🧠 Final Tips

* Don’t run everything as **root** user.
* Only open the ports you really need.
* Use a separate user (e.g. `nodeuser`) to run your validator.
* Always secure your **mnemonic / private key** — don’t keep it on the server!

***

## 📦 The most frequently installed and used dependencies for operating a crypto node or validator.&#x20;

When running a crypto node or validator — especially in Cosmos, Substrate, or Ethereum-based chains. you’ll often need to install essential tools and libraries to compile code, run the software, or manage the server.

#### ⚙️ Essential System Packages

Install these on most Ubuntu 20.04/22.04 servers:

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y \
  curl wget git build-essential \
  jq make gcc tmux unzip \
  lz4 net-tools htop \
  ca-certificates software-properties-common
```

#### 🧰 Go (Golang)

Most Cosmos SDK chains require Go.

```bash
# Replace with the latest stable version if needed
wget https://golang.org/dl/go1.22.2.linux-amd64.tar.gz
sudo rm -rf /usr/local/go
sudo tar -C /usr/local -xzf go1.22.2.linux-amd64.tar.gz

# Add to PATH (for bash or zsh)
echo "export PATH=\$PATH:/usr/local/go/bin:\$HOME/go/bin" >> ~/.bashrc
source ~/.bashrc
```

#### 🔎 Verify:

```bash
go version
```

#### 🐍 Python (Optional for Some Tooling)

```bash
sudo apt install python3 python3-pip -y
```

#### 🪙 Rust (Common for Substrate chains)

```bash
curl https://sh.rustup.rs -sSf | sh
source $HOME/.cargo/env
```

#### 🔎 Verify:

```bash
rustc --version
```

#### 📚 Optional But Useful Tools

| Tool        | Purpose                            | Install Command              |
| ----------- | ---------------------------------- | ---------------------------- |
| `screen`    | Run processes in background        | `sudo apt install screen`    |
| `htop`      | Visual system resource monitor     | `sudo apt install htop`      |
| `jq`        | JSON parser used in scripts        | `sudo apt install jq`        |
| `lz4`       | For snapshot decompression         | `sudo apt install lz4`       |
| `unzip`     | Extract `.zip` files               | `sudo apt install unzip`     |
| `net-tools` | Port scanning and IP checks        | `sudo apt install net-tools` |
| `fail2ban`  | Basic security for SSH brute force | `sudo apt install fail2ban`  |

## 🐙 Using Git and Github&#x20;

Git is the version control tool used to manage code. GitHub is the website where most crypto node projects host their source code.

#### 📥 Cloning a Repository

```bash
git clone https://github.com/project/repo.git
cd repo
```

> This will download the entire codebase to your server.

#### 📈 Checking the Status

```bash
git status            # Show file changes and branch info
git remote -v         # Show GitHub repo links
git branch            # Show current branch
```

#### 🔄 Pulling Updates

```bash
git pull origin main
```

> Use this to get the latest code updates from GitHub (for example, when a new binary is released).

If you’re unsure which branch the project uses:

```bash
git branch -r         # Show remote branches
```

#### 🧪 Switching Branches

```bash
git checkout testnet-branch-name
```

> Useful when a project has separate branches for testnet, mainnet, or dev environments.

#### 🔧 Building After Pull

After pulling new code, you often need to rebuild:

```bash
make install
# OR
go build -o binary-name .
```

#### 🧹 Cleaning Build Files (Optional)

```bash
make clean
```

#### 🆕 Creating Your Own Git Repo (Advanced)

If you're building your own tooling or automation scripts:

```bash
git init                          # Start a new Git repo
git remote add origin <url>       # Connect to GitHub
git add .                         # Stage all files
git commit -m "initial commit"    # Save changes
git push -u origin main           # Push to GitHub
```

***

## **🧹 Uninstalling Apps or Binaries**

Sometimes you need to remove a binary or app from your system — maybe the node software has changed, or you're switching networks. Here's how to safely uninstall things on Ubuntu.

#### &#x20;1. Uninstall Software Installed via `apt` 📦

```bash
sudo apt remove packagename
sudo apt purge packagename         # Also remove config files
sudo apt autoremove                # Remove unused dependencies
```

📌 _Example:_

```bash
sudo apt remove golang-go
sudo apt purge tmux
```

#### 2. Remove Go Binaries Installed from Source 🧱

If you built a node binary with `make install`, it usually ends up in `$HOME/go/bin`.

```bash
which binary-name                  # Find path
rm $(which binary-name)           # Remove the binary
```

📌 _Example:_

```bash
rm $(which seid)
```

Or manually:

```bash
rm ~/go/bin/binary-name
```

***

#### 3. Delete the Source Code Folder 📁&#x20;

If you cloned from GitHub and no longer need the code:

```bash
rm -rf ~/repo-folder
```

📌 _Example:_

```bash
rm -rf sei-chain
```

***

#### 4. Clear Configuration & Data (if needed) 🧼&#x20;

Most blockchain nodes store their data and config in a `.chain` folder (e.g. `.sei`, `.gaia`, `.celestia-app`).

```bash
rm -rf ~/.chain-folder
```

📌 _Example:_

```bash
rm -rf ~/.sei
```

***

#### 5. Remove systemd Service (if used)🧹&#x20;

If you used `systemd` to manage your node:

```bash
sudo systemctl stop nodename
sudo systemctl disable nodename
sudo rm /etc/systemd/system/nodename.service
sudo systemctl daemon-reload
```

***

✅ _That’s it! Your system is now clean._

> Tip: Keep a record of everything you installed for each node in case you need to clean up or reinstall later.
