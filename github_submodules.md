---
title: HowTo - Github submodules
category: github
tags:
- github
---

Update all submodules (need to have the same 'main' branch):  
git submodule foreach git pull origin main

git add project/submodule_proj_name
git commit -m 'gitlink to submodule_proj_name was updated'
git push

## Pull a repo with submodules
git clone git@github.com:AllenInstitute/BarcodeTender-pipeline
cd BarcodeTender-pipeline
git submodule update --init

