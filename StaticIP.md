# How to set static IP in Linux via netplan
- open terminal
- write the following commands:
  sudo su
  cd /etc/netplan/
- write the command "nano" followed by the new file name.
  file name requires:
  1. starts with a number like the followes: 01,02,03 and so on the bigger the number the later it will be executed.
  2. end with ".yaml" extension

For example:
  nano 01-staticip.yaml

- in the file write the following. replace any {} with the info needed:
  network:
  version: 2
  renderer: networkd
  ethernets:
    {netname}:
      dhcp4: no
      addresses: [{static_ip}/24]
      routes:
        - to: 0.0.0.0/0
          via: {gateway_ip}
      nameservers:
        addresses: [{dns_server_1}, {dns_server_2}]

  For example:
  network:
  version: 2
  renderer: networkd
  ethernets:
    ens192:
      dhcp4: no
      addresses: [192.168.0.117/24]
      routes:
        - to: 0.0.0.0/0
          via: 192.168.0.1
      nameservers:
        addresses: [8.8.8.8, 1.1.1.1]
  The netname is mostly ens192.
  
