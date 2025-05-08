---
description: Gensyn Testnet Node Guide ( Train AI )
---

# Gensyn

### 💻 System Requirements

| Requirement                    | Details                                            |
| ------------------------------ | -------------------------------------------------- |
| **CPU Architecture**           | `arm64` or `amd64`                                 |
| **Recommended RAM**            | 24 GB                                              |
| **CUDA Devices (Recommended)** | `RTX 3090`, `RTX 4070`, `RTX 4090`, `A100`, `H100` |
| **Python Version**             | Python >= 3.10 (For Mac, you may need to upgrade)  |

### 📥 Installation

1. **for the ubuntu culture XD**

```bash
sudo apt update && sudo apt upgrade -y
```

2. **Install other dependencies**

```bash
sudo apt update && sudo apt install -y python3 python3-venv python3-pip curl wget screen git lsof nano unzip iproute2
```

3. **Install Node.js and npm**

```bash
curl -sSL https://raw.githubusercontent.com/zunxbt/installation/main/node.sh | bash
```

4. **Install CUDA & nvcc**



5. **Create a `screen` session**

```
screen -S gensyn
```
