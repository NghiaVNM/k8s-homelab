# 1. information
OS: Rocky Linux 10.1 (Red Quartz)

# 2. Install
```
  dnf install epel-release
  dnf install wireguard-tools
```

# 3. Setup server
```
  sysctl -w net.ipv4.ip_forward=1
  mkdir -p /etc/wireguard/vpn-gateway-1
  wg genkey | tee /etc/wireguard/vpn-gateway-1/vpn-gateway-1.key | wg pubkey | tee /etc/wireguard/vpn-gateway-1/vpn-gateway-1.pub
  systemctl enable wg-quick@vpn-gateway-1
  systemctl start wg-quick@vpn-gateway-1
  wg show
```
```
# /etc/sysctl.conf

net.ipv4.ip_forward=1
```

```
# /etc/wireguard/vpn-gateway-1.conf
# vpn-gateway-1
[Interface]
PrivateKey = <key>
Address = 10.8.0.2/24

# vpn-server
[Peer]
PublicKey = <pub>
Endpoint = <ip>:51820
AllowedIPs = 10.8.0.0/24
PersistentKeepalive = 25
```