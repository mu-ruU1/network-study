# Ansible

## Install Ansible

```bash
$ sudo apt update
$ sudo apt install -y software-properties-common
$ sudo apt-add-repository --yes --update ppa:ansible/ansible
$ sudo apt install -y ansible
```

## 事前準備

```
en
conf t

hostname R1
username admin password admin

ip domain-name example.com

crypto key generate rsa
  1024

ip ssh version 2
```

## 参考

- [Ansible Core Documentation](https://docs.ansible.com/core-translated-ja.html)
- [Ansible - Cisco.Ios](https://docs.ansible.com/ansible/latest/collections/cisco/ios/index.html#plugins-in-cisco-ios)
