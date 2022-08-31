[![DEVNET](https://upload.wikimedia.org/wikipedia/en/f/f8/CiscoDevNet2.png)](https://developer.cisco.com)

# Ansible - playbook to automate template synchronization between central GIT repository of templates and DNAC Template project

## Features
- Leverages Ansible-galaxy DNAC collection (https://galaxy.ansible.com/cisco/dnac)
- Depends on dnacentersdk
- clones specified GIT repository of templates
- for each template, synchronizes its content to DNAC Template Project
- for each template, adds commit message to template summary:comments section
- for each templates, adds comment section with the file last diff to template payload

For demonstration purposes, the following sample public git repo of templates was used as a reference: https://github.com/imanassypov/dnac_git_templates

Once a change to the git repo is detected and playbook is run, the changes from the repo will get synchronized to the referenced DNAC instance

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

## Sample result of template content rendering in DNAC
In the screenshot below, the following elements have been provisioned by the Ansible playbook:
- template files 'mgmt_loopback.j2', and 'snmp_template.j2' with their respective content synchronized to the sample git template repository here: https://github.com/imanassypov/dnac_git_templates
- template comments header automatically generated to reflect diff from the last version of the same template
- template version and the commit message of the author describing modifications in human readable form

[![DEVNET](https://github.com/imanassypov/ansible-git-dnac/blob/main/sample_run.png)](https://github.com/imanassypov/ansible-git-dnac/blob/main/sample_run.png)

## References
- This work has been inspired by the CICD Pipeline Demo with DNA Center by Oliver Boehmer, https://gitlab.com/oboehmer/dnac-template-as-code
- Ansible DNA Center Galaxy module collection, https://cisco-en-programmability.github.io/dnacenter-ansible/main/plugins/index.html#description
- DNA Center API reference, https://developer.cisco.com/docs/dna-center/
