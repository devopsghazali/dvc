MLOps Data Versioning & Cloud Sync Setup
Is project mein humne DVC (Data Version Control) ka use kiya hai taaki hum apne data ko version kar sakein aur use Google Cloud Storage (GCS) par backup kar sakein.

Step 1: Initialize DVC
Project directory mein DVC ko initialize karein:

Bash


dvc init --no-scm
Step 2: Google Cloud Bucket ko Connect karein
Apni Google Cloud Storage bucket ko remote storage ke taur par add karein:

Bash


dvc remote add -d myremote gs://<YOUR_BUCKET_NAME>/dvc-storage
Step 3: Service Account Authentication
Google Cloud ke saath secure connection ke liye Service Account JSON file ka path setup karein:

Environment variable set karein (Windows PowerShell):

PowerShell


$env:GOOGLE_APPLICATION_CREDENTIALS="C:\path\to\your\service-account.json"
DVC config file (.dvc/config) ko verify karein ki usme sirf core aur remote URL ho:

Ini, TOML


['core']
    remote = myremote

['remote "myremote"']
    url = gs://<YOUR_BUCKET_NAME>/dvc-storage
Step 4: Data ko Track aur Push karein
Jab bhi aap koi nayi file ya dataset add karein:

Data track karein:

Bash


dvc add <data_file_or_folder>
Data ko Cloud Bucket par push karein:

Bash


dvc push
Step 5: Data Pull karna
Nayi machine par ya kisi aur directory mein data wapas lane ke liye:

Bash


dvc pull
Note: Hamesha apni service-account.json file ko .gitignore mein rakhein taaki wo Git repository par push na ho aur security bani rahe.
