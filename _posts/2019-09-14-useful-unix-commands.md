---
layout: post
category: Misc
title: Useful unix commands
tagline: by SunHaozhe
tags: 
  - Common knowledge
mathjax: true
comments: true
published: true
---

************************************************************************************************

https://stackoverflow.com/questions/43702546/tensorboard-doesnt-show-all-data-points 

```bash
tensorboard --samples_per_plugin scalars=0 --logdir xxx/
```

************************************************************************************************

For Mac OS, the `caffeinate` command is used to prevent a Mac from going to sleep. 

```bash
# stay until you tell the command to stop running 
# or close the terminal
caffeinate 

# wait for the process with ID 41734 to finish
caffeinate -w 41734  

# 18000 is the timeout value in seconds 
caffeinate -t 18000  

# Option -d prevents the display from sleeping.
# Option -i prevents the system from idle sleeping.
# Option -s prevents the system from sleeping. 
# Option -s is valid only when system is running on AC power.
# Some other options also exist. 
```

************************************************************************************************

To get the summary of a grand total disk usage size of an directory in "Human Readable Format": 

```bash
du -sh *
# 1.8G	XXX
```

************************************************************************************************

On Mac OS, check CPU temperature (this needs to be installed `sudo gem install istats`)

```bash
istats 
```

************************************************************************************************

On Mac OS, change the default shell to Zsh

```bash
chsh -s /bin/zsh
```

On Mac OS, change the default shell to Bash

```zsh
chsh -s /bin/bash
```

************************************************************************************************

Check sum on Mac OS

```zsh
# user manual
shasum --help

# check sha1 sum 
shasum -a 1 [file_name]
```



************************************************************************************************












