import os
import re
import requests

#### Auth token from Zenodo Applications page
atk = <ZONODO_AUTH_TOKEN>

#### Create a new upload entry and get the bucket URL
headers = {'Content-Type': 'application/json'}
params = {'access_token': atk}
r = requests.post('https://zenodo.org/api/deposit/depositions',
                  params = params,
                  json = {},
                  headers = headers)

bucket_url = r.json()['links']['bucket']

#### Walk the target directory to get all files to upload
base_dir = '/mnt/barware-manuscript/BarWare-demo/'

files = []
for r,d,f in os.walk(base_dir):
  for file in f:
    # Remove files starting with .git if a git repo is involved.
    if '.git' not in r:
      files.append(os.path.join(r,file))

#### Upload each file to the Zenodo bucket URL/filename
for path in files:
    filename = re.sub(base_dir,'',path)
    with open(path, "rb") as fp:
      r = requests.put('%s/%s' % (bucket_url, filename), data = fp, params = params)

#### Find upload later for updates
r = requests.get('https://zenodo.org/api/deposit/depositions', 
                 params = {'q': 'BarWare Cell Hashing Pipeline Demonstration',
                           'access_token':atk})

uid = r.json()[0]['id']

#### Make a new version

r = requests.post('https://zenodo.org/api/deposit/depositions/' + str(uid) + '/actions/newversion',
                  params = {'access_token':atk})

#### Remove previous files
r = requests.get('https://zenodo.org/api/deposit/depositions/' + str(uid) + '/files',
                 params={'access_token': atk})

for entry in r.json():
  id = entry['id']
  r = requests.delete('https://zenodo.org/api/deposit/depositions/' + str(uid) + '/files/' + id, 
                      params = {'access_token':atk})

#### Upload new files

r = requests.get('https://zenodo.org/api/deposit/depositions/' + str(uid) + '?access_token=' + atk)
bucket_url = r.json()['links']['bucket']

params = {'access_token':atk}
 
fileset = ['BarWare-pipeline.zip', 'cellranger.zip', 'demo_output.zip', 'fastq.zip', 'demo_sample_sheet.csv', 'demo_well_sheet.csv']
for filename in fileset:
    with open(dir + filename, "rb") as fp:
        r = requests.put(bucket_url + '/' + filename, data = fp, params = params)

