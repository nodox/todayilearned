# IAM service account access to GCS buckets in another project

Today I learned you can give an IAM service account in **Project B** access to a 
Google Cloud storage bucket in **Project A**.

- Get the IAM service account email address from Project B: `robot@project-b.iam.gserviceaccount.com`
- Find GCS Bucket in Project A
- Go to Permissions tab
- Click Add Members
- Paste service account email in *New members* field
- Add the proper GCS role (Admin, Viewer, Creator, etc)
