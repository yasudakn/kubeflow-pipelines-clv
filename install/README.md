# Configuring AI Platform Pipelines

1. Select or create a GCP project. You must be [Project Owner](https://cloud.google.com/iam/docs/understanding-roles) to complete the configuration.
2. Enable Cloud Services utilzed by the pipelines. In addition to the services [enabled by default](https://cloud.google.com/service-usage/docs/enabled-service) you need to enable the following additional services:
```
PROJECT_ID=[YOUR PROJECT ID]

gcloud config set project $PROJECT_ID

gcloud services enable \
cloudbuild.googleapis.com \
container.googleapis.com \
cloudresourcemanager.googleapis.com \
iam.googleapis.com \
containerregistry.googleapis.com \
containeranalysis.googleapis.com \
automl.googleapis.com
 

```
   - Compute Engine
   - Cloud Storage
   - Container Registry
   - Kubernetes Engine
   - BigQuery
   - AutoML 
   - Cloud Build
   - Cloud Resource Manager
1. You can enable the services using **GCP Console** or by executing the `enable_apis.sh` script in the `/install` folder.
1. Open a new session in **Cloud Shell**
1. Create a working directory and clone this repo.
1. Edit the `terraform.tfvars` file to provide your values for the configuration's parameters:

Parameter | Description
----------|------------
project_id|Project ID of the GCP project you selected for the solution
cluster_name| The name of the GKE cluster to create. 
cluster_location | The zone for the cluster. Since AutoML only support` us-central1` it is recommended to create the cluster in one of the zones in the same region
bucket_name | The name of the GCS bucket that will be used as an artifact storage. Terraform will attempt to create the bucket so make sure that the bucket under this name does not exist.


1. In Cloud Shell, in the `/install/terraform` folder execute the following commands:
```
terraform init
terraform apply
```

To clean up, execute `terraform destroy` from the `/install/terraform` folder.

To deploy the pipelines and the pipeline's artifacts follow the instructions in the [README](../deploy/README.md) in the `/deploy` folder.





