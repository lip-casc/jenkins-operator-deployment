# jenkins-operator-deployment
Jenkins-operator deployment on Kubernetes.

This repository is based on jenkins official documentation: [https://jenkinsci.github.io/kubernetes-operator/](https://jenkinsci.github.io/kubernetes-operator/)


## Requirements

To run Jenkins Operator, you will need:

- access to a **Kubernetes** cluster version **1.11+**
- **kubectl** version **1.11+**


## Configure Custom Resource Definition

The Custom Resource Definition (CRD) API has been introduced to Kubernetes in v1.7 and it enables users to add custom APIs to their Kubernetes cluster which can be used like any other native Kubernetes objects. Defining a CRD object creates a new custom resource with a name and schema that you specify. The Kubernetes API serves and handles the storage of your custom resource.

Install Jenkins Custom Resource Definition:

    kubectl apply -f https://raw.githubusercontent.com/jenkinsci/kubernetes-operator/master/deploy/crds/jenkins_v1alpha2_jenkins_crd.yaml


## Deploy Jenkins Operator Using YAML’s

Create a namespace for the operator:

    kubectl create namespace jenkins

Apply Service Account and RBAC roles:

    kubectl -n jenkins apply -f https://raw.githubusercontent.com/jenkinsci/kubernetes-operator/master/deploy/all-in-one-v1alpha2.yaml

Watch Jenkins Operator instance being created:

    kubectl -n jenkins get pods -w


## Create PVC

Run the following command:

    kubectl -n jenkins create -f pvc.yaml

## Deploy Jenkins Instance

Once Jenkins Operator is up and running let’s deploy the actual Jenkins instance. Use the **jenkins_instance.yaml** located in the repository:

    kubectl -n jenkins create -f jenkins_instance.yaml
