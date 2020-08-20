# Load Testing AI Platform Prediction for Online Serving

This directory contains code samples that demonstrate how to test and monitor AI Platform Prediction online serving performance with respect to:
1. Service latency
2. CPU, GPU, and Memory Utilization 
3. Auto-scaling

We use [Locust](locust.io) to simulate the user prediction requests workload. 

The code samples utilize the [ResNet101 image classification model](https://tfhub.dev/google/imagenet/resnet_v2_101/classification/4) from TensorFlow Hub. 
The design patterns and techniques demonstrated in the samples can be easily adapted to other domains and types of models.

## The repo content:
[01-prepare-and-deploy.ipynb](01-prepare-and-deployipynb). This notebook shows how to prepare a [TensorFlow SavedModel](https://www.tensorflow.org/guide/saved_model) for 
serving and deploy to AI Platform Prediction. The notebook covers:
 * Re-using pre-trained models from TensorFlow Hub
 * Enhancing a pre-trained model with pre-processing and post-processing graphs
 * Defining multiple serving signatures
 * Deploying the SavedModel to AI Platform Prediction with auto-scaling and GPUs
 * Validate deployed model versions

[02-perf-testing.ipynb](02-perf-testing.ipynb). This notebook demonstrates how to use [Locust](locust.io), [Google Kubernetes Engine](https://cloud.google.com/kubernetes-engine) and [Cloud Monitoring](https://cloud.google.com/monitoring) to perform load testing of model versions deployed in AI Platform Prediction. 
The notebook covers:
* Deploying Locust to a [GKE cluster](https://cloud.google.com/kubernetes-engine)
* Creating custom [Cloud Monitoring](https://cloud.google.com/monitoring) dashboards
* Preparing and running load tests
* Retrieving and consolidating test results

[03-analyze-results.ipynb](03-analyze-results.ipynb). This notebook outlines techniques for analyzing load test results. 
The notebook covers:
* Aligning and normalizing metric time series
* Using Pandas and Matplotlib to analyze and visualize test results

[monitoring-template.json](monitoring-template.json). This is an example template of a custom [Cloud Monitoring dashboard](https://cloud.google.com/monitoring/dashboards) that demonstrates how to aggregate the standard [AI Platform Prediction metrics](https://cloud.google.com/monitoring/api/metrics_gcp#gcp-ml) with custom [Cloud Logging log-based metrics](https://cloud.google.com/logging/docs/logs-based-metrics) based on Locust test statistcs.

[locust](locust). This folder contains [Kustomize](https://kustomize.io/) manifests to deploy Locust to a GKE cluster and a [locustfile](https://docs.locust.io/en/stable/writing-a-locustfile.html) script demonstrating how to load test the AI Platform Prediction REST API `predict` method.

[test](test). This folder contains the artifacts required for running the load test, and sample results produced of the test.


## Environment setup

1. Create a [Cloud Storage bucket](https://cloud.google.com/storage/docs/creating-buckets).
2. Create a [Cloud Monitoring Workspace](https://cloud.google.com/monitoring/workspaces/create) in your project.
3. Create an [AI Notebooks instance](https://cloud.google.com/ai-platform/notebooks/docs/create-new) TensorFlow 2.2.
4. Open the JupyterLab from the AI Notebook instance.
5. Open a new Terminal to execute the following commands to clone the repository:
    ```
    git clone https://github.com/GoogleCloudPlatform/mlops-on-gcp
    cd mlops-on-gcp/model_serving/caio-load-testing
    ```



