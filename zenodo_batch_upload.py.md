import os
import re
import requests

# Auth token from Zenodo Applications page
atk = <ZONODO_AUTH_TOKEN>

# Create a new upload entry and get the bucket URL
headers = {'Content-Type': 'application/json'}
params = {'access_token': atk}
r = requests.post('https://.zenodo.org/api/deposit/depositions',
                  params = params,
                  json = {},
                  headers = headers)

bucket_url = r.json()['links']['bucket']

# Walk the target directory to get all files to upload
base_dir = '/mnt/barware-manuscript/BarWare-demo/'

files = []
for r,d,f in os.walk(base_dir):
  for file in f:
    # Remove files starting with .git if a git repo is involved.
    if '.git' not in r:
      files.append(os.path.join(r,file))

# Upload each file to the Zenodo bucket URL/filename
for path in files:
    filename = re.sub(base_dir,'',path)
    with open(path, "rb") as fp:
      r = requests.put('%s/%s' % (bucket_url, filename), data = fp, params = params)

