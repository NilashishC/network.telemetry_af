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
        name: network.telemetry.setup_nxos

```

**Note:** This collection comes with setup data pre-loaded in vars/main.yaml for setup_collection & setup_nxos roles. To override those, you can provide an YAML file with all the required variables and run your playbook by passing `-e collector_setup_data=<path to setup data file>` & `-e nxos_setup_data=<path to setup data file>`.

### Sample collector setup data file

An example collector setup data file is available [here](https://github.com/NilashishC/network.telemetry/blob/main/roles/setup_collector/vars/main.yml).


### See Also:

* [Ansible Using collections](https://docs.ansible.com/ansible/latest/user_guide/collections_using.html) for more details.

## Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) to see the full text.