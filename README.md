# Ubuntu Playbooks
---
## Create an inventory

```
cat << EOF > hosts.yml
---
  all:
    hosts:
      ansibletest03:
      ansibletest04:
EOF
```
---
## Join AD

### Create vars required by playbook:
```
cat << EOF > vars.yml
match_host: all
ADAdminGroup: "admingroup"
ADDomain: "domain"
ADJoinUsername: "aduser"
ADJoinPassword: "adpassword"
EOF
```

### Troubleshooting
Delete sssd cache:
```
systemctl stop sssd; rm -rf /var/lib/sss/{db,mc}/*; systemctl start sssd
```

### Run the playbook:
```
ansible-playbook -i hosts.yml -e @vars.yml join_ad.yml
```
---
## Disable multipathd for VMware storage
```
ansible-playbook -i hosts.yml -e match_host=all disable_multipathd_vmware.yml
```
---
## Deploy Crowdstrike

### Create vars required by playbook:
```
cat << EOF > vars.yml
match_host: all
crowdstrike_http_url: http://your_http_file_server.yourdomain.tld/falcon-sensor_6.43.0-14005_amd64.deb
CID: 00000000000000000000000000000000-00
EOF
```

### Run the playbook:
```
ansible-playbook -i hosts.yml -e @vars.yml deploy_crowdstrike.yml
```
