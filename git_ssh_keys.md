---
title: Github SSH Keys
category: github
tags:
- github
---

Steps to generate and use an SSH key for authentication with Github.


On the target machine:  

Generate a key:  
`ssh-keygen -t ed25519 -C "lucasg@alleninstitute.org"`

Start ssh-agent:  
`eval "$(ssh-agent -s)"`

Add the key:  
`ssh-add ~/.ssh/id_ed25519`

Add the SSH key to your Github account:  
https://github.com/settings/keys  
`nano ~/.ssh/id_ed25519`  

Test connection:  
`ssh -T git@github.com`

Instead of:  
`git clone https://github.com/aifimmunology/tenx-atacseq-pipeline`  
Use:  
`git clone git@github.com:aifimmunology/tenx-atacseq-pipeline`  

For R:  
install.packages("credentials")
