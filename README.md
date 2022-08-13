# Ubuntu Playbooks

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

### Run the playbook:
```
ansible-playbook -i hosts.yml -e @vars.yml join_ad.yml
```