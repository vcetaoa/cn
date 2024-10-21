
# Basic Networking Commands in Linux

This guide covers various essential networking commands in Linux, commonly used for network diagnostics and configuration.

## 1. **ping**
The `ping` command checks the network connectivity between the host and a remote machine. It sends ICMP Echo Request messages and waits for Echo Replies.

**Usage:**
```bash
ping [destination]
```

Example:
```bash
ping google.com
```

## 2. **traceroute (tracert)**
`traceroute` traces the route that packets take to reach a destination. It helps diagnose where connectivity issues occur along the path.

**Usage:**
```bash
traceroute [destination]
```

Example:
```bash
traceroute google.com
```

## 3. **nslookup**
The `nslookup` command queries DNS to obtain domain name or IP address mapping information.

**Usage:**
```bash
nslookup [domain]
```

Example:
```bash
nslookup google.com
```

## 4. **netstat**
`netstat` displays network connections, routing tables, interface statistics, masquerade connections, and multicast memberships.

**Usage:**
```bash
netstat
```

Example to list all listening ports:
```bash
netstat -l
```

## 5. **ARP**
`arp` manipulates the kernel's ARP (Address Resolution Protocol) table, which maps IP addresses to MAC addresses.

**Usage:**
```bash
arp -a
```

To add a static ARP entry:
```bash
arp -s [IP] [MAC]
```

## 6. **RARP**
The `rarp` command is used for Reverse ARP. It resolves a MAC address into an IP address (opposite of ARP). This command is not widely used anymore, as it's been largely replaced by DHCP.

**Usage:**
```bash
rarp -a
```

## 7. **ip**
The `ip` command is a powerful tool for managing IP addresses, network interfaces, and routing tables.

**Usage:**
```bash
ip [options] [object] [command]
```

Example to show network interfaces:
```bash
ip addr
```

## 8. **ifconfig**
The `ifconfig` command is used to configure network interfaces. It is now mostly replaced by the `ip` command but still widely used.

**Usage:**
```bash
ifconfig [interface]
```

Example to bring an interface up:
```bash
ifconfig eth0 up
```

## 9. **dig**
The `dig` command queries DNS servers for information. It’s useful for testing DNS resolution and diagnosing DNS issues.

**Usage:**
```bash
dig [domain]
```

Example to query A records for a domain:
```bash
dig google.com
```

## 10. **route**
`route` shows or manipulates the IP routing table.

**Usage:**
```bash
route
```

Example to view the routing table:
```bash
route -n
```

## Conclusion
These basic networking commands are crucial for managing and troubleshooting network configurations and connections in Linux environments.
