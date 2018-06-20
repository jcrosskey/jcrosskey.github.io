---
layout: post
title:  "Remove yatta from eclipse"
categories: eclipse, bash
---
I installed Yatta and its eclipse plugin following the instructions on their website, thought it would be
a great tool to manage eclipse profiles. But I did not expect it to keep popping up and refuse to shut down
when I tried again and again. What's more annoying is that, I cannot seem to remove it. It was like a ghost
that kept coming back. 

To get an idea of where the yatta related files are located, use the command `locate yatta`. You can then see
all the files are located in `$HOME/.eclipse` and `$HOME/Library`. After locating the evil files, next step is natually
find and remove:

```bash
find $HOME/.eclipse -name *yatta* -exec rm -rf {} \;
find $HOME/Library -name *yatta* -exec rm -rf {} \;
```

Tada, no more yatta!
