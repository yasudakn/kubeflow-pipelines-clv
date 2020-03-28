# Starting pipeline runs

There are three ways to trigger runs of the example pipelines:
- Using the Kubeflow Pipelines UI
- Using the KFP CLI tool
- Using the KFP SDK `kfp.Client()` API


### Running the pipelines using Kubeflow Pipelines UI

Use the procedure described in [Pipelines Quickstart](https://www.kubeflow.org/docs/pipelines/pipelines-quickstart/) to create experiments and submit pipeline runs.

The compiled training pipeline has been stored by Cloud Build in the following GCS location:

`gs://[_BUCKET_NAME][_PIPELINES_FOLDER]/[_TRAIN_PIPELINE].tar.gz`

The compiled batch predict pipeline is in

`gs://[_BUCKET_NAME][_PIPELINES_FOLDER]/[_PREDICT_PIPELINE].tar.gz`

In addition, both pipelines have been uploaded to your AI Platform Pipelines instance.

The sample training and testing datasets can be found in:

`gs://[_BUCKET_NAME][_SAMPLE_DATASET]`

The runtime parameters required by the pipelines are described in detail in [`/pipelines/README.md`](/pipelines/README.md)

Most of the parameters have reasonable default values that don't have to be modified during the intial runs.

### Running the pipelines using the KFP CLI tool

The [KFP CLI tool](https://www.kubeflow.org/docs/pipelines/sdk/sdk-overview/) enables you to use a subset of the Kubeflow Pipelines SDK directly from the command line. 

To start a run of the *CLV Continuous Training* pipeline:
```
```

To start a run of the *CLV Batch Predict* pipeline:
```
```


### Running the pipelines using KFP SDK

You can also use the `kfp.Client()` API from the [KFP SDK](https://www.kubeflow.org/docs/pipelines/sdk/sdk-overview/) to upload pipelines to a KFP environment, create experiments, and start runs.





