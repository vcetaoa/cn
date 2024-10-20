**EXP_3**

# Network Setup Instructions

## 1. Prepare the Devices
- Take **3 PCs** and **1 Switch** (Cisco 2960).

## 2. Assign IP Addresses to the PCs
- All PCs should be in the same network, so configure their IP addresses as follows:
  - **PC0**: IP address `192.168.1.2`, Subnet mask `255.255.255.0`
  - **PC1**: IP address `192.168.1.3`, Subnet mask `255.255.255.0`
  - **PC3**: IP address `192.168.1.4`, Subnet mask `255.255.255.0`

## 3. Set Default Gateway
- For all PCs, set the **default gateway** to `192.168.1.1`.

## 4. Configure the Switch

Access the **Switch CLI** and perform the following configuration:

```bash
Switch> enable
Switch# configure terminal
Switch(config)# interface vlan 1
Switch(config-if)# ip address 192.168.1.1 255.255.255.0
Switch(config-if)# no shutdown
Switch(config-if)# exit

Switch(config)# line vty 0 4
Switch(config-line)# password abc
Switch(config-line)# login
Switch(config-line)# exit

Switch(config)# enable password abc1

```
**NOW GO TO CMD OF PC3**

**Telnet from PC3**

```
telnet 192.168.1.1
```
**Enter the password abc when prompted**
```
User Access Verification

Password: 
```

```
Switch> enable
#Enter the enable password abc1 when prompted:
Password: 

```
- Configure FastEthernet 0/1 Interface
```
Switch# configure terminal
Switch(config)# interface fastethernet 0/1
Switch(config-if)# shutdown
Switch(config-if)# no shutdown
```
**This completes the Telnet configuration.**
