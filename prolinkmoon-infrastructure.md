---
description: explained how prolinkmoon manage infra & some tools for community
---

# Prolinkmoon Infrastructure

Prolinkmoon - professional DevOps ready/standby for manage and monitoring infra 24/7. We rely on scripts, so that make it easy and everything runs automatically, but not forgetting security and reliability. &#x20;

For now we operate just some Node and Validator (5-15 network) and focus on what we have. Our target is to operate the Top 1-60 Cosmos Ecosystem and several other L1/L2 networks.

## Cosmos Ecosystem

Every single Network we run 3 main node, Validator, Relay, and back-up +(TMKSM for high availability key).

<figure><img src=".gitbook/assets/Prolinkmoon - infra.png" alt=""><figcaption><p>Prolinkmoon - infra</p></figcaption></figure>



### 1. Validator node&#x20;

**Dedicated, high-end server, high availability, secure and isolated.**  for validator nodes we ensure there are no trouble and we really maintain 99.9% up-time on the network. of course we have tools for monitoring and high security.

### 2. Relay node

**Dedicated / Shared instance, SS** = Secure and Services ✅.  The purpose or core of the relay node is to facilitate our Validator Node or other nodes. to help maintain the synchronization of the blockchain network by relaying data between different nodes, ensuring that all nodes have the latest information.

also for services / public consumption. we provide RPC, gRPC, p2p, State-Sync, API .etc is open to public. who ever can access Relay node.

### 3. Operator node

**Fully isolated & more secured.** Operator node is to operate TMKMS and stored the Validator keys / other important keys or files. We use TMKMS to avoid double-sign, high-availability keys and portable keys. TMKMS is standard for running in production. every validator on active-set must use it.

\| Validator << >> Operator node | we have important rules for security reason, to avoid malicious attack.



**Additional node:**

**-  Back-up**

in some cases we need backup nodes in case of simultaneous maintenance. but that is very rare, because relays and validators are quite robust and are not located in the same geographic or instance.

**-  Monitoring & Tools**&#x20;

We provide Explorer by Ping.Pub with Prolinkmoon RPC, API .etc. and also for monitoring Validator, Relay, Operator we use xxx by xxx. Actually Monitoring & Tools we can running on Relay(if any free space). but we chose to run on a different VM.&#x20;



**How Prolinkmoon manage cost-efficiency and avoid node bloat ?**&#x20;

## Prolinkmoon Playground

— a simple apps on Ubuntu for manage your node easily ( coming soon )



## Other Network

— a prolinkmoon infra for other Network ( Docs docs are being written 🛠 )

