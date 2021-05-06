#Overview
-----------------------------------------------------------------------------------------------------------------------------
Running websites can be difficult with all of the overhead of creating and managing VMs, clusters, pods, services, etc. This is fine for larger, multi-tiered applications, but if you are just trying to get your website deployed and visible, it's a lot of overhead.

With Cloud Run, Google Cloud's implementation of Google's KNative framework, you can manage and deploy your website without any of the infrastructure overhead you experience with a VM or pure Kubernetes-based deployments. Not only is this a simpler approach from a management perspective, it also gives you the ability to "scale to zero" when there are no requests coming into your website.

Cloud Run brings "serverless" development to containers and can be run either on your own Google Kubernetes Engine (GKE) clusters or on a fully managed PaaS solution provided by Cloud Run. You will be running the latter scenario in this lab.

The exercises are ordered to reflect a common cloud developer experience:

Create a Docker container from your application

Deploy the container to Cloud Run

Modify the website

Roll out a new version with zero downtime

Architecture diagram
Below you can see the flow of the deployment and Cloud Run hosting.

Begin with a Docker image created via Cloud Build, which gets triggered from Cloud Shell, then deploy the image out to Cloud Run from a command in Cloud Shell.

db5f05c090d5ebcb.png

What you'll learn
How to build a Docker image using Cloud Build and upload it to gcr.io

How to deploy Docker images to Cloud Run

How to manage Cloud Run deployments

How to setup an endpoint for an application on Cloud Run

by Rajdeep Das
