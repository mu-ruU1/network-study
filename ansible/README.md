# Ansible

## Install Ansible

```bash
$ sudo apt update
$ sudo apt install -y software-properties-common
$ sudo apt-add-repository --yes --update ppa:ansible/ansible
$ sudo apt install -y ansible
```

## 事前準備

### ルーター

```
!
en
conf t
!
hostname R1
username admin password admin
!
enable password admin
!
line vty 0 4
login local
transport input ssh
!
ip domain-name example.com
!
crypto key generate rsa modulus 1024
!
ip ssh version 2
!
end
!
```

### 接続元 (IOS バージョンによっては不要)

```bash
Host 192.168.255.*
  KexAlgorithms +diffie-hellman-group1-sha1
  HostkeyAlgorithms +ssh-rsa
  PubkeyAcceptedAlgorithms +ssh-rsa
```

## 参考

- [Ansible Core Documentation](https://docs.ansible.com/core-translated-ja.html)
- [Ansible - Cisco.Ios](https://docs.ansible.com/ansible/latest/collections/cisco/ios/index.html#plugins-in-cisco-ios)
