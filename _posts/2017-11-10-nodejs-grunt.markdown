---
layout: post
title:  "Setting up for grunt on Ubuntu"
categories: nodejs, grunt, npm, web
---
**Setting up for grunt** 

```bash
# install nodejs
curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
sudo apt-get install nodejs
node -v

# Ensure that npm is up-to-date
sudo npm update -g npm

# Install grunt CLI
sudo npm install -g grunt-cli

# Install some grunt-init templates
git clone https://github.com/gruntjs/grunt-init-gruntfile.git ~/.grunt-init/gruntfile

# Create project-specific package.json file automatically using grunt-init
grunt-init gruntfile

# Add Grunt and grunt plugins to an existing package.json
npm install grunt --save-dev
```
### References
* [Installing Node.js via package manager](https://nodejs.org/en/download/package-manager/)
* [Getting started with grunt](https://gruntjs.com/getting-started)



