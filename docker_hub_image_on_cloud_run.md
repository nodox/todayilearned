# How to run a Docker Hub image on Google Cloud Run

To run a default Docker Hub image on Google Cloud Run, 
you need to download the image locally, rename it, 
and then push it to your GCR repository.

Did this while trying to run a Ghost container from Docker Hub.


```
docker pull ghost:3.14
docker tag ghost:3.14 us.gcr.io/$PROJECT_NAME/ghost:3.14
docker push us.gcr.io/$PROJECT_NAME/ghost:3.14
```
