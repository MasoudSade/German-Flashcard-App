# WireGuard VPN Setup Guide

## 🔒 Private Home Hosting with WireGuard VPN

This guide helps you set up a secure VPN to access your German Flashcard App hosted at home.

---

## 📋 What You'll Need

- **Home Server:**
  - Raspberry Pi (recommended) OR
  - Old laptop/PC running Linux OR
  - Windows PC with WSL2

- **Network Requirements:**
  - Router with port forwarding capability
  - Public IP address (static or dynamic with DDNS)

- **Time Required:** 2-3 hours for first-time setup

---

## Part 1: Install WireGuard Server

### On Ubuntu/Debian (Raspberry Pi or Server)

```bash
# Update system
sudo apt update && sudo apt upgrade -y

# Install WireGuard
sudo apt install wireguard -y

# Enable IP forwarding
echo "net.ipv4.ip_forward=1" | sudo tee -a /etc/sysctl.conf
sudo sysctl -p
```

### On Windows (with WSL2)

```powershell
# Install WSL2 first if not already installed
wsl --install

# Then in WSL terminal:
sudo apt update && sudo apt install wireguard -y
```

---

## Part 2: Generate Keys

### Server Keys

```bash
# Navigate to WireGuard directory
cd /etc/wireguard

# Generate server private key
sudo wg genkey | sudo tee server_private.key

# Generate server public key
sudo cat server_private.key | wg pubkey | sudo tee server_public.key

# Secure the keys
sudo chmod 600 server_private.key
```

**Save these keys!** You'll need them for configuration.

```bash
# Display server keys
echo "Server Private Key:"
sudo cat server_private.key
echo ""
echo "Server Public Key:"
sudo cat server_public.key
```

### Client Keys (for each device)

Generate keys for each device you want to connect:

```bash
# Client 1 (e.g., phone)
wg genkey | tee client1_private.key | wg pubkey > client1_public.key

# Client 2 (e.g., laptop)
wg genkey | tee client2_private.key | wg pubkey > client2_public.key

# Display client keys
echo "Client 1 Private Key:"
cat client1_private.key
echo ""
echo "Client 1 Public Key:"
cat client1_public.key
```

---

## Part 3: Configure WireGuard Server

### Create Server Configuration

```bash
# Create config file
sudo nano /etc/wireguard/wg0.conf
```

### Server Configuration Template

```ini
[Interface]
# Server's VPN IP address
Address = 10.0.0.1/24

# WireGuard listening port
ListenPort = 51820

# Server's private key (replace with your actual key)
PrivateKey = SERVER_PRIVATE_KEY_HERE

# Enable packet forwarding and NAT
PostUp = iptables -A FORWARD -i wg0 -j ACCEPT; iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE; ip6tables -A FORWARD -i wg0 -j ACCEPT; ip6tables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
PostDown = iptables -D FORWARD -i wg0 -j ACCEPT; iptables -t nat -D POSTROUTING -o eth0 -j MASQUERADE; ip6tables -D FORWARD -i wg0 -j ACCEPT; ip6tables -t nat -D POSTROUTING -o eth0 -j MASQUERADE

# Client 1 (Phone)
[Peer]
# Client's public key
PublicKey = CLIENT1_PUBLIC_KEY_HERE
# Client's VPN IP
AllowedIPs = 10.0.0.2/32

# Client 2 (Laptop)
[Peer]
PublicKey = CLIENT2_PUBLIC_KEY_HERE
AllowedIPs = 10.0.0.3/32

# Add more peers as needed
```

**Important:**
- Replace `SERVER_PRIVATE_KEY_HERE` with your server private key
- Replace `CLIENT1_PUBLIC_KEY_HERE` with each client's public key
- Change `eth0` to your network interface name (check with `ip a`)

### Find Your Network Interface

```bash
# List network interfaces
ip a

# Common names:
# - eth0 (Ethernet)
# - wlan0 (WiFi)
# - ens33 (Some systems)
```

### Save and Exit

Press `Ctrl+X`, then `Y`, then `Enter`

---

## Part 4: Start WireGuard Server

```bash
# Start WireGuard
sudo wg-quick up wg0

# Check status
sudo wg show

# Enable on boot
sudo systemctl enable wg-quick@wg0
```

You should see output like:
```
interface: wg0
  public key: YOUR_SERVER_PUBLIC_KEY
  private key: (hidden)
  listening port: 51820
```

---

## Part 5: Configure Firewall

### Using UFW (Ubuntu Firewall)

```bash
# Install UFW if not installed
sudo apt install ufw -y

# Allow SSH (IMPORTANT - don't lock yourself out!)
sudo ufw allow 22/tcp

# Allow WireGuard port
sudo ufw allow 51820/udp

# Enable firewall
sudo ufw enable

# Check status
sudo ufw status
```

### Using iptables Directly

```bash
# Allow WireGuard
sudo iptables -A INPUT -p udp --dport 51820 -j ACCEPT

# Save rules
sudo apt install iptables-persistent -y
sudo netfilter-persistent save
```

---

## Part 6: Set Up Dynamic DNS (If No Static IP)

### Using DuckDNS (Free & Easy)

1. **Create Account:**
   - Visit https://www.duckdns.org
   - Sign in with GitHub or Google

2. **Create Subdomain:**
   - Enter subdomain name (e.g., `myhome`)
   - You get: `myhome.duckdns.org`
   - Note your token

3. **Install DuckDNS Updater:**

```bash
# Create directory
mkdir -p ~/duckdns
cd ~/duckdns

# Create update script
cat > duck.sh << 'EOFSCRIPT'
#!/bin/bash
echo url="https://www.duckdns.org/update?domains=YOUR_SUBDOMAIN&token=YOUR_TOKEN&ip=" | curl -k -o ~/duckdns/duck.log -K -
EOFSCRIPT

# Replace YOUR_SUBDOMAIN and YOUR_TOKEN with your actual values
nano duck.sh

# Make executable
chmod +x duck.sh

# Test it
./duck.sh
cat duck.log  # Should show "OK"
```

4. **Automate Updates:**

```bash
# Add to crontab (runs every 5 minutes)
crontab -e

# Add this line:
*/5 * * * * ~/duckdns/duck.sh >/dev/null 2>&1
```

### Alternative: No-IP

1. Sign up at https://www.noip.com
2. Create hostname
3. Install Dynamic Update Client:

```bash
cd /usr/local/src/
sudo wget http://www.noip.com/client/linux/noip-duc-linux.tar.gz
sudo tar xf noip-duc-linux.tar.gz
cd noip-2.1.9-1/
sudo make install
sudo noip2 -C  # Configure
sudo noip2  # Start
```

---

## Part 7: Configure Router Port Forwarding

### Find Your Router IP

```bash
# On Linux/Mac
ip route | grep default

# On Windows
ipconfig | findstr "Gateway"
```

Usually: `192.168.1.1` or `192.168.0.1`

### Access Router Admin Panel

1. Open browser and go to router IP (e.g., `http://192.168.1.1`)
2. Login with admin credentials

### Add Port Forwarding Rule

**Settings vary by router, but generally:**

1. Find **Port Forwarding** or **Virtual Server** section
2. Add new rule:
   ```
   Service Name: WireGuard
   External Port: 51820
   Internal IP: YOUR_SERVER_LOCAL_IP (e.g., 192.168.1.100)
   Internal Port: 51820
   Protocol: UDP
   Status: Enabled
   ```

### Find Your Server's Local IP

```bash
# On your server
hostname -I

# Or
ip addr show | grep "inet "
```

### Find Your Public IP

```bash
curl ifconfig.me
# Or visit: https://www.whatismyip.com
```

---

## Part 8: Set Up Web Server

### Option A: Simple Python Server

```bash
# Navigate to flashcard directory
cd /path/to/German-Flashcard-App

# Start web server
python3 -m http.server 8080

# Keep running in background
nohup python3 -m http.server 8080 &
```

### Option B: Nginx (Recommended for 24/7)

```bash
# Install Nginx
sudo apt install nginx -y

# Create directory for your app
sudo mkdir -p /var/www/flashcards

# Copy your files
sudo cp -r /path/to/German-Flashcard-App/* /var/www/flashcards/

# Create Nginx configuration
sudo nano /etc/nginx/sites-available/flashcards
```

Add this configuration:

```nginx
server {
    listen 80;
    server_name localhost;

    root /var/www/flashcards;
    index flashcard.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

Enable the site:

```bash
# Link configuration
sudo ln -s /etc/nginx/sites-available/flashcards /etc/nginx/sites-enabled/

# Test configuration
sudo nginx -t

# Restart Nginx
sudo systemctl restart nginx
sudo systemctl enable nginx
```

---

## Part 9: Configure WireGuard Clients

### Android/iOS Client

1. **Install WireGuard:**
   - **Android:** Google Play Store
   - **iOS:** Apple App Store

2. **Create Client Configuration:**

Create a file named `client1.conf`:

```ini
[Interface]
# Client's VPN IP address
Address = 10.0.0.2/24

# Client's private key
PrivateKey = CLIENT1_PRIVATE_KEY_HERE

# DNS server (optional)
DNS = 8.8.8.8, 8.8.4.4

[Peer]
# Server's public key
PublicKey = SERVER_PUBLIC_KEY_HERE

# Your public IP or DuckDNS hostname:port
Endpoint = YOUR_PUBLIC_IP_OR_DDNS:51820

# Route only VPN traffic (or use 0.0.0.0/0 for all traffic)
AllowedIPs = 10.0.0.0/24

# Keep connection alive
PersistentKeepalive = 25
```

3. **Import Configuration:**
   - Open WireGuard app
   - Tap "+" → "Create from file" or "Scan QR code"
   - Select the config file or scan QR code (see below)

### Generate QR Code for Easy Mobile Setup

```bash
# Install qrencode
sudo apt install qrencode -y

# Generate QR code from config
sudo cat /etc/wireguard/client1.conf | qrencode -t ansiutf8

# Or save as image
sudo cat /etc/wireguard/client1.conf | qrencode -o client1_qr.png
```

Scan this QR code with your mobile WireGuard app!

### Windows/Mac/Linux Client

1. **Install WireGuard:**
   - **Windows:** https://www.wireguard.com/install/
   - **Mac:** `brew install wireguard-tools`
   - **Linux:** `sudo apt install wireguard`

2. **Copy Configuration:**
   - Save `client1.conf` to your computer

3. **Import Configuration:**
   - **Windows/Mac:** Open WireGuard app → Add Tunnel → Import from file
   - **Linux:**
     ```bash
     sudo cp client1.conf /etc/wireguard/
     sudo wg-quick up client1
     ```

---

## Part 10: Testing the Connection

### On Server

```bash
# Check WireGuard status
sudo wg show

# You should see connected peers:
# peer: CLIENT_PUBLIC_KEY
#   endpoint: CLIENT_IP:PORT
#   latest handshake: X seconds ago
```

### On Client

1. **Connect to VPN:**
   - Open WireGuard app
   - Toggle connection ON
   - Should show "Active" or "Connected"

2. **Test VPN Connection:**
   ```bash
   # Ping server's VPN IP
   ping 10.0.0.1
   ```

3. **Access Flashcard App:**
   - Open browser
   - Go to: `http://10.0.0.1:8080/flashcard.html`
   - (Or `http://10.0.0.1` if using Nginx)

---

## Part 11: Security Hardening

### Change Default Port

```bash
# Edit server config
sudo nano /etc/wireguard/wg0.conf

# Change ListenPort from 51820 to something else (e.g., 51234)
ListenPort = 51234

# Update router port forwarding accordingly
```

### Disable Root Login (SSH)

```bash
sudo nano /etc/ssh/sshd_config

# Find and set:
PermitRootLogin no
PasswordAuthentication no  # Use key-based auth only

sudo systemctl restart sshd
```

### Install Fail2Ban

```bash
sudo apt install fail2ban -y
sudo systemctl enable fail2ban
sudo systemctl start fail2ban
```

### Regular Updates

```bash
# Create update script
cat > ~/update_system.sh << 'EOF'
#!/bin/bash
sudo apt update
sudo apt upgrade -y
sudo apt autoremove -y
EOF

chmod +x ~/update_system.sh

# Add to weekly cron
sudo crontab -e
# Add: 0 3 * * 0 /home/YOUR_USERNAME/update_system.sh
```

---

## 📱 Client Configuration Examples

### Complete Android/iOS Config

```ini
[Interface]
Address = 10.0.0.2/24
PrivateKey = yAnz5TF+lXXJte14tji3zlMNq+hd2rYUIgJBgB3fBmk=
DNS = 8.8.8.8

[Peer]
PublicKey = HIgo9xNzJMWLKASShiTqIybxZ0U3wGLiUeJ1PKf8ykw=
Endpoint = myhome.duckdns.org:51820
AllowedIPs = 10.0.0.0/24
PersistentKeepalive = 25
```

### Complete Linux/Windows Config

```ini
[Interface]
Address = 10.0.0.3/24
PrivateKey = cNf44TF+lYYJte15tji4zlMOq+hd3rYUIgKBgC4fCnl=
DNS = 8.8.8.8, 8.8.4.4

[Peer]
PublicKey = HIgo9xNzJMWLKASShiTqIybxZ0U3wGLiUeJ1PKf8ykw=
Endpoint = myhome.duckdns.org:51820
AllowedIPs = 10.0.0.0/24
PersistentKeepalive = 25
```

---

## 🐛 Troubleshooting

### Connection Issues

**Problem:** Can't connect to VPN

**Solutions:**
1. Check WireGuard is running:
   ```bash
   sudo systemctl status wg-quick@wg0
   ```

2. Verify port forwarding:
   - Check router settings
   - Test port: https://www.yougetsignal.com/tools/open-ports/

3. Check firewall:
   ```bash
   sudo ufw status
   sudo ufw allow 51820/udp
   ```

4. Verify public IP is correct:
   ```bash
   curl ifconfig.me
   ```

### Can Connect to VPN but Can't Access Apps

**Problem:** VPN connects but can't access web server

**Solutions:**
1. Check web server is running:
   ```bash
   sudo systemctl status nginx
   # Or for Python:
   ps aux | grep python
   ```

2. Test locally on server:
   ```bash
   curl http://localhost:8080
   ```

3. Check IP forwarding:
   ```bash
   cat /proc/sys/net/ipv4/ip_forward
   # Should show: 1
   ```

4. Verify firewall allows local network:
   ```bash
   sudo ufw allow from 10.0.0.0/24
   ```

### Slow Connection

**Solutions:**
1. Use UDP (default)
2. Reduce MTU in client config:
   ```ini
   [Interface]
   MTU = 1420
   ```

3. Check your internet speed:
   ```bash
   speedtest-cli
   ```

---

## 📊 Useful Commands

```bash
# Check WireGuard status
sudo wg show

# Show detailed peer info
sudo wg show wg0

# Restart WireGuard
sudo wg-quick down wg0 && sudo wg-quick up wg0

# View WireGuard logs
sudo journalctl -u wg-quick@wg0 -f

# Check connected clients
sudo wg show wg0 peers

# Test port is open
sudo netstat -tulpn | grep 51820

# Monitor traffic
sudo tcpdump -i wg0

# View firewall rules
sudo iptables -L -n -v
```

---

## 🔄 Adding New Devices

1. **Generate new client keys:**
   ```bash
   wg genkey | tee client3_private.key | wg pubkey > client3_public.key
   ```

2. **Add peer to server config:**
   ```bash
   sudo nano /etc/wireguard/wg0.conf
   ```
   Add:
   ```ini
   [Peer]
   PublicKey = CLIENT3_PUBLIC_KEY
   AllowedIPs = 10.0.0.4/32
   ```

3. **Restart WireGuard:**
   ```bash
   sudo wg-quick down wg0 && sudo wg-quick up wg0
   ```

4. **Create client config** and import on device

---

## 📚 Resources

- **WireGuard Official:** https://www.wireguard.com
- **DuckDNS:** https://www.duckdns.org
- **No-IP:** https://www.noip.com
- **Port Check:** https://www.yougetsignal.com/tools/open-ports/
- **WireGuard Tools:** https://www.wireguard.com/tools/

---

## ✅ Final Checklist

- [ ] WireGuard installed on server
- [ ] Keys generated (server + clients)
- [ ] Server configuration created
- [ ] WireGuard service running
- [ ] Firewall configured
- [ ] Port forwarding set up on router
- [ ] Dynamic DNS configured (if needed)
- [ ] Web server running (Nginx or Python)
- [ ] Client configurations created
- [ ] VPN connection tested
- [ ] Can access flashcard app via VPN

---

**Success! You now have a secure private VPN to access your flashcard app from anywhere! 🔒**
