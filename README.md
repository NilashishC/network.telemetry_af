# Ansible Collection - network.telemetry

An Ansible Collection to build, and maintain Telemetry stack using Telegraf, InfluxDB and Grafana for network appliances.

## Installation
```
pip install ansible-core
ansible-galaxy collection install git+https://github.com/NilashishC/network.telemetry.git
```

## Usage
```yaml
---
- hosts: collector
  gather_facts: yes
  tasks:
    - ansible.builtin.include_role:
        name: network.telemetry.setup_collector

```
```yaml
---
- hosts: network_appliances
  gather_facts: yes
  tasks:
    - ansible.builtin.include_role:
        name: network.telemetry.setup_telemetry

```

**Note:** This collection comes with setup data pre-loaded in vars/main.yaml for collector setup role. 
To override those, you can provide an YAML file with all the required variables and run your playbook
by passing `-e collector_setup_data=<path to setup data file>`.

### See Also:

* [Cisco NX-OS Platform Options](https://docs.ansible.com/ansible/latest/network/user_guide/platform_nxos.html)
* [Ansible Using collections](https://docs.ansible.com/ansible/latest/user_guide/collections_using.html) for more details.

## Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) to see the full text.