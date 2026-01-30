# 💻 Internet Income - Passive Bandwidth Sharing

<img src="https://i.ibb.co/DKbwPN1/imgonline-com-ua-twotoone-2ck-Xl1-JPvw2t-D1.jpg" width="100%" height="300"/>

Earn passive income by sharing your internet bandwidth through Docker containers. Supports multiple proxies, VPNs, and IP addresses.

**Disclaimer:** This is an advanced fork. Use at your own risk.

---

## 🆕 What's New

- **Honeygain Auto-Pot**: Automatically claims your daily lucky pot rewards
- **Custom Device Names**: Use `honeygain_names.txt` or auto-generate random names
- **Earnapp Improved**: No more daily restarts, better stability
- **Wizardgain Support**: New platform added

---

## 🚀 Quick Start

### 1. Install Docker
```bash
sudo bash internetIncome.sh --install
```

### 2. Configure
Edit `properties.conf` with your credentials:
```bash
nano properties.conf
```

**Important:** 
- Wrap credentials in single quotes: `'your@email.com'`
- Enable network mode: `USE_PROXIES=true` or `USE_DIRECT_CONNECTION=true`
- Leave empty any apps you don't want to use

### 3. Optional: Custom Honeygain Names
Edit `honeygain_names.txt` with one name per line, or let the script auto-generate random names.

### 4. Start
```bash
sudo bash internetIncome.sh --start
```

---

## 📋 Supported Platforms

**Passive Earning Apps:**
- Honeygain (with auto-pot grabbing)
- Earnapp (improved stability)
- Wizardgain (new!)
- IPRoyals Pawns
- PacketStream
- Peer2Profit
- Repocket
- Traffmonetizer
- BitPing
- ProxyRack
- ProxyBase
- Proxylite
- EarnFM
- Gaganode
- Titan Network
- URnetwork
- Nodepay
- Wipter
- Antgain

**Browser-Based:**
- Mysterium
- Uprock

---

## ⚙️ Basic Configuration

**Direct Connection:**
```bash
USE_DIRECT_CONNECTION=true
```

**With Proxies:**
```bash
USE_PROXIES=true
```
Create `proxies.txt`:
```
socks5://user:pass@host:port
http://user:pass@host:port
```

**Honeygain with Auto-Pot:**
```bash
HONEYGAIN_EMAIL='your@email.com'
HONEYGAIN_PASSWORD='yourpassword'
HONEYGAIN_POT=true
```

**Wizardgain:**
```bash
WIZARDGAIN_EMAIL='your@email.com'
```

**Earnapp:**
```bash
EARNAPP=true
```

---

## 🔧 Commands

```bash
# Start containers
sudo bash internetIncome.sh --start

# Stop containers
sudo bash internetIncome.sh --stop

# Restart containers
sudo bash internetIncome.sh --restart

# Delete containers (keeps device IDs)
sudo bash internetIncome.sh --delete

# Delete everything including backups
sudo bash internetIncome.sh --deleteBackup

#restart containers starting with set name 
# example 
sudo bash restart.sh --restart container_prefix/earnapp/wizardgain/etc

```

---

## 📊 Monitoring

After starting, check these files for access URLs:
- `earnapp.txt` - Add these URLs to your Earnapp dashboard
- `mysterium.txt` - Mysterium node access

View running containers:
```bash
sudo docker ps
```

---

## 🐛 Troubleshooting

**Containers won't start?**
```bash
sudo bash internetIncome.sh --delete
sudo bash internetIncome.sh --start
```

**Port conflicts?** The script auto-finds available ports.

**Proxy issues?** Verify format: `protocol://user:pass@host:port`

---

## 📁 Key Files

- `internetIncome.sh` - Main script
- `properties.conf` - Your configuration
- `proxies.txt` - Proxy list (if using proxies)
- `honeygain_names.txt` - Custom Honeygain device names (optional)
- `earnapp.txt` - Generated Earnapp URLs
- `*-data/` folders - Persistent data (preserved on delete)

---

## 💡 Tips

1. Use quality residential proxies for better earnings
2. Enable multiple apps - they pay for different traffic types
3. Enable `HONEYGAIN_POT=true` for extra Honeygain earnings
4. Check dashboards regularly to ensure containers are running
5. Start small and scale up as you learn

---


## ⚠️ Disclaimer

This script is provided "as is" without warranty. Use at your own risk. Ensure you comply with all platform terms of service.

---

**Original Repository:** [engageub/InternetIncome](https://github.com/engageub/InternetIncome)
