# Getting started

## install Node.js
https://github.com/nodesource/distributions/blob/master/README.md
### Installation instructions
Node.js v14.x:
```bash
# Using Ubuntu
curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -
sudo apt-get install -y nodejs

# Using Debian, as root
curl -sL https://deb.nodesource.com/setup_14.x | bash -
apt-get install -y nodejs
```

## Install Hexo
We can install Hexo  by running

npm install -g hexo

Now you are ready to hexo your own blog! First, start with

hexo init [your website folder name]

this will initialize a repository under [your website folder name]. To spin up a default Hexo website, do

cd [your website folder name]
hexo generate

This will generate the static files (html, css, etc) for your website with hexo default options. You can now view your website on local hosting by running

hexo server

you will see output similar to the following

    INFO Start processing INFO Hexo is running at http://localhost:xxxx . Press Ctrl+C to stop.

