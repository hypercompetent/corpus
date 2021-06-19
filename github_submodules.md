---
title: HowTo - Github submodules
category: github
tags:
- github
---

Update all submodules (need to have the same 'main' branch):  
`git submodule foreach git pull origin main`

git add project/submodule_proj_name
git commit -m 'gitlink to submodule_proj_name was updated'
git push
