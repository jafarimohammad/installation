# installing nodejs in Centos
```
wget https://rpm.nodesource.com/setup_14.x
chmod +x setup_14.x
./setup_14.x
yum -y install nodejs

# check version
node -v
npm -v

# configure user permission
npm -g config set user root 

# installing Development Tools
yum groupinstall "Development Tools"

# installing Gatsby
npm install -g gatsby-cli

# create new template project
gatsby new gatsby_project

# build project
cd gatsby_project
gatsby build
```
