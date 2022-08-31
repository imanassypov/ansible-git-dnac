[![DEVNET](https://upload.wikimedia.org/wikipedia/en/f/f8/CiscoDevNet2.png)](https://developer.cisco.com)

# Ansible - playbook to automate template synchronization between central GIT repository of templates and DNAC Template project

## Features
- Leverages Ansible-galaxy DNAC collection (https://galaxy.ansible.com/cisco/dnac)
- Depends on dnacentersdk
- clones specified GIT repository of templates
- for each template, synchronizes its content to DNAC Template Project
- for each template, adds commit message to template summary:comments section
- for each templates, adds comment section with the file last diff to template payload

## Tested with
```
python --version
Python 3.9.13
```
```
ansible --version
ansible [core 2.13.3]
  config file = None
  configured module search path = ['/Users/imanassy/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /Users/imanassy/Documents/Ansible/Ansible-git-DNAC/venv/lib/python3.9/site-packages/ansible
  ansible collection location = /Users/imanassy/.ansible/collections:/usr/share/ansible/collections
  executable location = /Users/imanassy/Documents/Ansible/Ansible-git-DNAC/venv/bin/ansible
  python version = 3.9.13 (main, Aug 20 2022, 16:35:59) [Clang 13.1.6 (clang-1316.0.21.2.5)]
  jinja version = 3.1.2
  libyaml = True
```

### Installation
Create virtual env for dependencies
```
python3 -m venv env
source env/bin/activate
```

Install DNA Center SDK
```
pip install dnacentersdk
```

```
ansible-galaxy collection install cisco.dnac
```

### Update configuration to match your environment
Modify 'credentials.yml' and 'hosts' files to match your execution environment. Variable values should be self explanatory in the example provided

## Sample execution
```
ansible-playbook -i ansible-git-dnac/hosts ansible-git-dnac/ansible-git-dnac.yml
```

