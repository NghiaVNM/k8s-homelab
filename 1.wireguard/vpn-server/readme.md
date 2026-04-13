# 1. information
OS: Ubuntu 22.04.4 LTS

# 2. Install
```
  apt install wireguard
```

# 3. Setup
```
  sysctl -w net.ipv4.ip_forward=1
  ip link add dev wg-vpn type wireguard
  ip address add dev wg-vpn 10.8.0.1/24
  mkdir -p /etc/wireguard/vpn-server
  wg genkey | tee /etc/wireguard/vpn-server/vpn-server.key | wg pubkey | tee /etc/wireguard/vpn-server/vpn-server.pub
  wg setconf wg-vpn /etc/wireguard/vpn-server.conf
  ip link set up dev wg-vpn
  wg show
  systemctl enable wg-quick@vpn-server
  systemctl status wg-quick@vpn-server
```
```
# /etc/sysctl.conf

net.ipv4.ip_forward=1
```

```
# /etc/wireguard/vpn-server.conf

[Interface]
PrivateKey = <key>
ListenPort = 51820
```