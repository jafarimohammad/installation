# install Gitlab-ce in Centos7
```
wget https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh
chmode +x script.rpm.sh
yum -y install gitlab-ce

# Configure external_url
vim /etc/gitlab/gitlab.rb

# Reconfigure gitlab-ce
gitlab-ctl reconfigure

# default password
cat /etc/gitlab/initial_root_password
```
