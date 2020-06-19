# ansible-role-create-ct

Role Ansible pour créer des conteneurs LXC sous Proxmox.

Avec le playbook fourni on crée tout les conteneurs du groupe lxc, pour limité l'exécution du playbook vous pouvez utiliser l'option `-l ct_name`

### playbooks/create_ct.yml
```yaml
- hosts: lxc
  connection: ssh
  gather_facts: no
  roles:
    - createct
    - ssh_install
```

### playbooks/vars/pve_credentials.yml
```yaml
user_pve: root@pam
passwd_pve: strongpass
host_pve: pve.elukerio.org
```

### group_vars/lxc.yml
```yaml
to_install: vim,net-tools,nmap,dnsutils,ferm,unattended-upgrades,apt-listchanges,wget,curl,git
proxy_ip: "2001:bc8:32d7:1509::f00d"
```

### host_vars/vault.yml
```yaml
ct_passwd: strongpass
```

### host_vars/atalante.yml
```yaml
---
# [Zeus ; Jupiter]
ct_node : sigma
node_bastion: minos
ct_vmid: 110
ct_name: test3
ct_onboot: 0
ct_if: vmbr1
#[20 -> DMZ ; 30 -> LOC ; 50 -> ADMIN ; 60 -> DIRTY]
ct_vlan: 20
#[2001:bc8:32d7:1509 ; fd2e:9d2b:16eb:VLAN]
ct_prefix6: "2001:bc8:32d7:1509"
ct_prefix4: "10.0.0"
ct_storage: local-zfs
#ct_cpus: 1
#ct_ram: 512
#ct_disk: 1
#ct_swap: 0
#ct_unprivileged: 1
```
