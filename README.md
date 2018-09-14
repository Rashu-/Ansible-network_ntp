# Network NTP Settings

Ansible role that defines ntp servers for networking devices. 

The configuration of the role is done so that it shouldn't be necessary to modify the role for any configuration.
All settings can configured by changing role parameters or by declaring new config as variable.

Please report any issues or send PR.

## Examples

```yaml
---

- name: Example of how to add an ntp server
  hosts: switches
  vars:
    ntp_servers:
      - name: 0.pool.ntp.org
        prefer: enabled
        state: present
  roles:
    - Ansible-network_ntp


- name: Example of how to add an ntp server with ntp source interface loopback0
  hosts: switches
  vars:
    ntp_servers:
      - name: 0.pool.ntp.org
        prefer: enabled
        state: present
    ntp_options:
      source:                         
        source_interface: loopback0      
        state: present
  roles:
    - Ansible-network_ntp

- name: Example of how to add an ntp server and ntp source address 192.168.1.1
  hosts: switches
  vars:
    ntp_servers:
      - name: 0.pool.ntp.org
        prefer: enabled
        state: present
    ntp_options:
      source:
        source_address: 192.168.1.1
        state: present
  roles:
    - Ansible-network_ntp

- name: Example of how to remove an ntp server
  hosts: switches
  vars:
    ntp_servers:
      - name: 1.1.1.1
        prefer: enabled
        state: absent
  roles:
    - Ansible-network_ntp


- name: Example of how to add a couple ntp servers with specific vrf 
  hosts: switches
  vars:
    ntp_servers:
      - name: 0.pool.ntp.org
        prefer: enabled
        state: present
        vrf: management
      - name: 1.1.1.1
        prefer: enabled
        state: present
        vrf: management
  roles:
    - Ansible-network_ntp

- name: Example of how to add ntp options
  hosts: switches
  vars:
    ntp_options:
      logging: yes
      master: no
      state: present
      stratum: 8               # when master=yes, stratum can be specified, default 8.
  roles:
    - Ansible-network_ntp
```

## Role variables

```yaml
# Define source address/interface(either one, not both) for ntp  (see README for examples)
ntp_options: { }

# Define the ntp servers to be configured (see README for examples)
ntp_servers: { }
```


## License

Apache


## Author

Dan Murarasu
