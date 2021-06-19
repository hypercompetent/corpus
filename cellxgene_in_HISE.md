---
title: HowTo - cellxgene in HISE
category: howto
tags:
- cellxgene
- HISE
---

## Run cellxgene in a HISE IDE

0. Install cellxgene  
`pip install cellxgene`  
1. Sign up for ngrok (ngrok.com - free tier will give you 1 URL at a time)  
2. Install ngrok:  
```
wget https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-linux-amd64.zip \
&& unzip ngrok-stable-linux-amd64.zip \
&& rm -f ngrok-stable-linux-amd64.zip
```
3. Add auth token from  
https://dashboard.ngrok.com/get-started/setup  
(will vary by user)  
4. launch cellxgene  
`cellxgene launch https://cellxgene-example-data.czi.technology/pbmc3k.h5ad`  
(for example dataset)  
5. run ngrok forwarding  
`./ngrok http 5005`  
6. open the forwarding URL shown in the ngrok display  
https://032c69bdb318.ngrok.io  
(example - will change each time)  
7. kill the ngrok process when you're done to close access  
(hit Ctrl-C in the ngrok terminal window)  

## Use your own .h5ad files

Thereafter, you'll just need to run steps 4-7:

4. launch cellxgene  
`cellxgene launch your_data.h5ad`  
(for example dataset)  
5. run ngrok forwarding  
`./ngrok http 5005`  
6. open the forwarding URL shown in the ngrok display  
https://032c69bdb318.ngrok.io  
(example - will change each time)  
7. kill the ngrok process when you're done to close access  
(hit Ctrl-C in the ngrok terminal window)  

