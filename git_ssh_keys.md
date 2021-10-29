---
title: HowTo - Github SSH Keys
category: howto
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
`cat ~/.ssh/id_ed25519.pub`  

Test connection:  
`ssh -T git@github.com`

Instead of:  
`git clone https://github.com/aifimmunology/tenx-atacseq-pipeline`  
Use:  
`git clone git@github.com:aifimmunology/tenx-atacseq-pipeline`  

To install packages:
```
git clone --branch=dev git@github.com:aifimmunology/ATAComb
sudo R --vanilla 'install.packages("ATAComb",s=T,r=NULL)'
```

To switch from HTTPS to SSH:
git remote set-url origin git@github.com:aifimmunology/ATAComb

In brief:
```
ssh-keygen -t ed25519 -C "lucasg@alleninstitute.org"
eval "$(ssh-agent -s)"
ssh-add /home/jupyter/.ssh/id_ed25519
cat /home/jupyter/.ssh/id_ed25519.pub
```
Go to Github and add the key:
https://github.com/settings/keys

Test connection:
```
ssh -T git@github.com
```





```
ssh-keygen -t ed25519 -C "elliott.swanson@alleninstitute.org"
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
cat ~/.ssh/id_ed25519.pub
```
Go to Github and add the key:
https://github.com/settings/keys

Test connection:
```
ssh -T git@github.com
```