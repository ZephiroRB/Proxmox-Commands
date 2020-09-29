# Proxmox Commands

# MANAGE LCX CHANGE ID
  pct enter ID
  pct stop ID
  pct start ID
  pct status ID

# Restore LCX CHANGE ID
  pct restore ID folder.lzo

# PATH DUMP BACKUP
  /var/lib/vz/dump/dump/

# RESIZE CHANGE ID
  pct resize ID rootfs 90G´

# ROUTING LCX TO SERVER PRIMARY CHANGE PORT AND IP
  iptables -t nat -A PREROUTING -i vmbr0 -p tcp -m tcp --dport port -j DNAT --to-destination ip:port
