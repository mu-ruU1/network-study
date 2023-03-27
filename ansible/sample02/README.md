```bash
 ansible all -i 192.168.255.1, -c ansible.netcommon.network_cli -u admin -k -m cisco.ios.ios_facts -e ansible_network_os=cisco.ios.ios
```
