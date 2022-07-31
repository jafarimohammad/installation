# installing Ansible in virtualenv python
```
yum install python-vertualenv
mkdir ansible
cd ansible
virtualenv venv-01
source bin/activate
pip install ansible
```
# config file with priority:
#  1. $ANSIBLE_CONFIG
#  2. ansible.cfg
#  3. ~/.ansible.cfg
#  4. /etc/ansible/ansible.cfg


# ansibe version
```
ansible --version
```
