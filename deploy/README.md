

## Building and deploying the pipelines

The process of building and deploying the pipelines and pipeline components has been automated using [GCP Cloud Build](https://cloud.google.com/cloud-build/docs/). The **Cloud Build** configuration is defined in the [cloudbuild.yaml](cloudbuild.yaml) file.

The build process goes through the following steps:
1. Create a docker image to support custom build steps
1. Build the base image for the lightweigh Python helper components. The name of the image is provided as a build parameter.
1. Build the image that hosts AutoML Tables components. The name of the image is provided as a build parameter.
1. Update the YAML specifications of the AutoML Tables components with the names of images the created  in the previous step.
1. Update the settings that control compilation. The values for these settings are provided as build parameters.
1. Compile the pipelines. 
1. Deploy the compiled pipelines to a GCS location. The path to the location is provided as a build parameter.
1. Deploy the artifacts used by the pipelines to a GCS location. The path to the location is provided as a build parameter.
1. Deploy the component images to the Container Registry of your project. 
1. Copy the sample dataset to a GCS location. The path to the location is provided as a build parameter.
1. Deploy compiled pipelines to your AI Platform Pipelines instance. 


You can configure the **Cloud Build** runs by creating a [Cloud Build trigger](https://cloud.google.com/cloud-build/docs/running-builds/create-manage-triggers) or you can start the runs manually using the `gcloud builds submit` command.

The `build.sh` script demonstrates how to use the `gcloud builds submit` command to start the build process. 

Make sure to update the `build.sh` with the settings reflecting your environment. Use the the following table as a guideline. 

Parameter | Description 
-----------|-------------
_BASE_IMAGE | The name of the base image for Lightweight Python compoments. Specify the image name only. The image will be pushed to `gcr.io/[YOUR_PROJECT_ID]/[_BASE_IMAGE]`
_AUTOML_TABLES_IMAGE | The name of the image that hosts AutoML Tables components
_TAG | The tag to apply when building images. Both images will be tagged with the same tag.
_TRAIN_PIPELINE | The name for the compiled training pipeline. The compiled pipeline is saved as `[_TRAIN_PIPELINE].tar.gz`
_PREDICT_PIPELINE | The name for the compiled batch predict pipeline. The compiled pipeline will be saved as `[_PREDICT_PIPELINE].tar.gz` |
_BUCKET_NAME | The GCS bucket created during installation of AI Platform Pipelines. The bucket name starts with the `hostedkfp-default-` prefix. 
_PIPELINES_FOLDER | The name of the folder in _BUCKET_NAME to store the compiled pipelines
_ARTIFACTS_FOLDER | The name of the folder in _BUCKET_NAME to store artificats used by the pipelines at running time. 
_SAMPLE_DATASET_FOLDER | The name of the folder in _BUCKET_NAME to store the sample dataset used by the pipelines.
_ENDPOINT | The endpoint to your AI Platform Pipelines instance. The endpoint to the AI Platform Pipelines instance can be found on the [AI Platform Pipelines](https://console.cloud.google.com/ai-platform/pipelines/clusters) page in the Google Cloud Console. Open the *SETTINGS* for your instance. Use the value of the `host` variable in the *Connect to this Kubeflow Pipelines instance from a Python client via Kubeflow Pipelines SKD* section of the *SETTINGS* window.|


The `/cloud-build/build.sh` demonstrates how to use `gcloud builds submit` to start the build process. 


### Folder structure

This folder contains Cloud Build artifacts:
- `cloudbuild.yaml` - a Cloud Build config file
- `build.sh` - a bash script template that uses `gcloud builds submit` to configure and start the build
- `kfp-builder/Dockerfile` - Dockerfile for the KFP CLI builder.

