# Nginx - Basics

## 🧭 NGINX – Basic Setup + Usage

NGINX is a web server that’s also commonly used as a **reverse proxy** — a tool to forward requests to services running on your server, like blockchain RPCs, APIs, dashboards, etc.

***

### 🛠️ Step 1: Install NGINX on Ubuntu

```bash
sudo apt update
sudo apt install nginx -y
```

Check if it’s running:

```bash
sudo systemctl status nginx
```

Start or enable if needed:

```bash
sudo systemctl start nginx
sudo systemctl enable nginx
```

***

### 🌐 Step 2: Allow HTTP/HTTPS Ports in Firewall

If you're using `ufw`, allow necessary ports:

```bash
sudo ufw allow 'Nginx Full'
```

***

### 🌍 Step 3: Basic Web Server Test

Open your server’s **public IP** in a browser, you should see the NGINX welcome page:

```
http://<your-server-ip>
```

***

### 🔁 Step 4: Using NGINX as Reverse Proxy (for RPC / API)

Let’s say your node’s **RPC** is running on:

```
http://localhost:26657
```

And you want to expose it via:

```
https://rpc.yourdomain.com
```

***

#### 📁 Create Config File for Subdomain

```bash
sudo nano /etc/nginx/sites-available/rpc.yourdomain.com
```

Paste this:

```nginx
server {
    listen 80;
    server_name rpc.yourdomain.com;

    location / {
        proxy_pass http://localhost:26657;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

***

#### 🔗 Enable the Site

```bash
sudo ln -s /etc/nginx/sites-available/rpc.yourdomain.com /etc/nginx/sites-enabled/
```

Then test and reload:

```bash
sudo nginx -t
sudo systemctl reload nginx
```

Now open: `http://rpc.yourdomain.com`

***

### 🔐 Step 5: Add Free SSL (HTTPS) with Certbot

Install Certbot and plugin for NGINX:

```bash
sudo apt install certbot python3-certbot-nginx -y
```

Run Certbot:

```bash
sudo certbot --nginx
```

Follow the instructions. Certbot will:

* Automatically get an SSL cert from Let's Encrypt
* Reload NGINX with secure HTTPS

To auto-renew:

```bash
sudo systemctl list-timers | grep certbot
```

***

### 🧪 Other Use Cases for NGINX

| Purpose           | Example                                     |
| ----------------- | ------------------------------------------- |
| Expose RPC        | `rpc.yourdomain.com -> localhost:26657`     |
| Expose Explorer   | `explorer.yourdomain.com -> localhost:3000` |
| Protect with auth | Use `auth_basic` in config                  |
| Rate limit RPC    | Use `limit_req` module                      |
| Proxy with HTTPS  | Add Certbot SSL on any service/subdomain    |

***

### 🧠 Tips

* Use separate files in `sites-available/` for each service.
* Always test config with: `sudo nginx -t`
* Reload NGINX after changes: `sudo systemctl reload nginx`
* Protect sensitive endpoints using IP allowlist or auth

***

💡 _NGINX makes it easy to manage many services on one VPS. It’s lightweight, powerful, and essential in modern DevOps._

Next → Learn to:

* Set up **Basic Authentication**
* Add **rate limiting to RPC endpoints**
* Run **multiple subdomains** on a single VPS
