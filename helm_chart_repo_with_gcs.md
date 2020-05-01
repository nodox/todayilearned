

### Requirements
- google cloud account
- gcloud cli
- helm
- git



## Create Google storage bucket
```
gsutil mb gs://majestic-miles/
```

## Create you working directory
```
mkdir -p majestic-miles/{stable,archives,scripts} && cd majestic-miles
git init
```

## Create a helm chart
```
helm create stable/demo
```

## Packages your chart
```
helm package -d archives stable/demo
```


## Create or Update your chart index
```
helm repo index majestic-miles --url https://majestic-miles.storage.googleapis.com --merge archives/index.yaml archives
```

- use the merge command to keep updating the index without overwriting previous entries. Good to keep history of packaged charts


## Upload your charts to GCS
```
gsutil rsync -d archives gs://majestic-miles
```

## Make your bucket public
```
gsutil iam ch allUsers:objectViewer gs://majestic-miles
```

- https://cloud.google.com/storage/docs/access-control/making-data-public#buckets


## Add repo to your cluster
```
helm repo add majestic-miles https://majestic-miles.storage.googleapis.com
```

Now you can install your chart using `helm install`

