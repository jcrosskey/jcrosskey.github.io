---
layout: post
title:  "HomeBrew Installed!"
categories: homebrew, macos
---
I'm setting up the new macbook slowly for everyday programming needs, thought I'd document some of the steps along the way so I don't have to search the internet all over again next time.

On my old laptop I have used MacPorts and remembered that it gave me a lot of headaches trying to manage what is what. After reading some articles comparing the package managers for macOS I decided to go with [Homebrew](https://brew.sh). If you are interested in the difference between them and need some help with deciding on which to install, here is a [link to a discussion on quora](https://www.quora.com/Should-I-use-Fink-MacPorts-Homebrew-or-something-else-for-MacOS-package-management-Which-are-most-popular-currently-Are-there-any-newer-players-worth-preferring-such-as-Rudix). Also another link discussing the [packages](https://www.quora.com/What-are-the-first-or-must-have-homebrew-packages-that-you-install-on-your-Mac) you might want to install after you install homebrew.

Installing homebrew is very easy, simply run this command: `/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`.

## Set up BasicTex using homebrew

When trying to use pandoc to convert markdown file to pdf, I followed [instructions from this link](https://pandoc.org/installing.html#macos) to install BasicTeX using command `brew install homebrew/cask/basictex`. However after the installation "completes", I still did not have `pdflatex`. This led me to the post [here](https://tex.stackexchange.com/questions/307483/setting-up-basictex-homebrew) to find the answer. In short there are two steps instead of the one shown in the pandoc's installation guide:

```bash
# ONLY downloads the .pkg installer
brew cask install basictex

# open the installer and install it following the instructions:
$ ls /usr/local/Caskroom/basictex/2018.0417
mactex-basictex-20180417.pkg
$ open /usr/local/Caskroom/basictex/2018.0417/mactex-basictex-20180417.pkg
```

Now open a new bash session,

```bash
$ which pdflatex
/Library/TeX/texbin/pdflatex
```

## Set up ruby and jekyll
The following is from [Jekyll on MacOS installation](https://jekyllrb.com/docs/installation/macos/).

```bash
xcode-select --install
brew install ruby
export PATH=/usr/local/opt/ruby/bin:$PATH # add to .bashrc
which ruby
ruby -v
gem install bundler jekyll
```
