#Deploy Kubernetes Load Balancer Service with Terraform
-----------------------------------------------------------------------------------------------------------------------

Qwiklabs Google Cloud Platform DevOps Essential Quest: Lab 04. Created by Rajdeep Das
----------------------------------------------------------------------------------------------------------------------------



Overview:

In Terraform, a Provider is the logical abstraction of an upstream API. This lab will show you how to setup a Kubernetes cluster and deploy Load Balancer type NGINX service on it.

Objectives
In this lab, you will learn how to:

Deploy a Kubernetes cluster along with a service using Terraform

Prerequisites
For this lab, you should have experience with the following:

Familiarity with Kubernetes Services
Familiarity with kubectl CLI.
Setup and Requirements
Before you click the Start Lab button
Read these instructions. Labs are timed and you cannot pause them. The timer, which starts when you click Start Lab, shows how long Google Cloud resources will be made available to you.

This Qwiklabs hands-on lab lets you do the lab activities yourself in a real cloud environment, not in a simulation or demo environment. It does so by giving you new, temporary credentials that you use to sign in and access Google Cloud for the duration of the lab.

Kubernetes Services
A service is a grouping of pods that are running on the cluster. Services are "cheap" and you can have many services within the cluster. Kubernetes services can efficiently power a microservice architecture.

Services provide important features that are standardized across the cluster: load-balancing, service discovery between applications, and features to support zero-downtime application deployments.

Each service has a pod label query which defines the pods which will process data for the service. This label query frequently matches pods created by one or more replication controllers. Powerful routing scenarios are possible by updating a service's label query via the Kubernetes API with deployment software.

Why Terraform?
While you could use kubectl or similar CLI-based tools mapped to API calls to manage all Kubernetes resources described in YAML files, orchestration with Terraform presents a few benefits:

You can use the same configuration language to provision the Kubernetes infrastructure and to deploy applications into it.
Drift detection - terraform plan will always present you the difference between reality at a given time and config you intend to apply.
Full lifecycle management - Terraform doesn't just initially create resources, but offers a single command to create, update, and delete tracked resources without needing to inspect the API to identify those resources.
Synchronous feedback - While asynchronous behavior is often useful, sometimes it's counter-productive as the job of identifying operation result (failures or details of created resource) is left to the user. e.g. you don't have IP/hostname of load balancer until it has finished provisioning, hence you can't create any DNS record pointing to it.
Graph of relationships - Terraform understands relationships between resources which may help in scheduling - e.g. Terraform won't try to create a service in a Kubernetes cluster until the cluster exists.
Update Terraform
The example code you will use in this lab requires Terraform versions 0.13.0 and higher.


//@uthor: Rajdeep Das
