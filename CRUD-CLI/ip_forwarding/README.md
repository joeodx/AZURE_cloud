# Script for ip forwarding 
**********************************

* IP forwarding is a networking function that allows a device, such as a router or a computer, to pass packets of data from one network interface to another.

```
#!/bin/bash

# configure iptables

echo "Configuring iptables..."

# Allow loopback traffic
sudo iptables -A INPUT -i lo -j ACCEPT
sudo iptables -A OUTPUT -o lo -j ACCEPT

# Allow established and related incoming connections
sudo iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

# Allow established outgoing connections
sudo iptables -A OUTPUT -m state --state ESTABLISHED -j ACCEPT

# Drop invalid incoming packets
sudo iptables -A INPUT -m state --state INVALID -j DROP

# Allow SSH incoming and outgoing connections
sudo iptables -A INPUT -p tcp --dport 22 -m state --state NEW,ESTABLISHED -j ACCEPT
sudo iptables -A OUTPUT -p tcp --sport 22 -m state --state ESTABLISHED -j ACCEPT

# Allow SSH into NVA only through the public subnet (app VM as a jumpbox)
# Must be done once the NVA's public IP address is removed
#sudo iptables -A INPUT -p tcp -s 10.0.2.0/24 --dport 22 -m state --state NEW,ESTABLISHED -j ACCEPT
#sudo iptables -A OUTPUT -p tcp --sport 22 -m state --state ESTABLISHED -j ACCEPT

# Allow SSH to other servers using the NVA as a jumpbox
# If need to make outgoing SSH connections with other servers from NVA
#sudo iptables -A OUTPUT -p tcp --dport 22 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
#sudo iptables -A INPUT -p tcp --sport 22 -m conntrack --ctstate ESTABLISHED -j ACCEPT

# Allow MongoDB traffic from public subnet to private subnet
sudo iptables -A FORWARD -p tcp -s 10.0.2.0/24 -d 10.0.4.0/24 --destination-port 27017 -m tcp -j ACCEPT

# Allow ICMP traffic from public subnet to private subnet
sudo iptables -A FORWARD -p icmp -s 10.0.2.0/24 -d 10.0.4.0/24 -m state --state NEW,ESTABLISHED -j ACCEPT

# Drop all other incoming and forwarding traffic by default
sudo iptables -P INPUT DROP
sudo iptables -P FORWARD DROP

echo "Done!"
echo ""

# make iptables rules persistent
# it will ask for user input by default

echo "Make iptables rules persistent..."
sudo DEBIAN_FRONTEND=noninteractive apt install iptables-persistent -y
echo "Done!"
echo ""

```