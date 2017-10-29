---
layout: post
title:  "Setting up for Jekyll Serving"
categories: jekyll, ruby, web
---
**Setting up for Jekyll Serving** 

### Install ruby and update the gems (ubuntu)
```bash
sudo apt-get install ruby-full
gem sudo gem update --system
sudo gem install jekyll bundler
```

### Create a new Jekyll site at ./myblog
```bash
jekyll new myblog
cd myblog
```

### Serve it up
```bash
bundle install
bundle exec jekyll serve
```
Now we can browse the webpage at `http://localhost:4000`.

### View webpage running on remote host
Use `ssh -L 9999:localhost:4000 remote_host_name` when ssh to the remote host, and browse at `http://localhost:9999`. Of course the ports can be freely changed.


### References
* [Jekyll's quick-start guide](https://jekyllrb.com/docs/quickstart/)

