# jenkins-operator-deployment
Jenkins-Operator deployment on Kubernetes.

This repository is based on jenkins official documentation: [https://jenkinsci.github.io/kubernetes-operator/](https://jenkinsci.github.io/kubernetes-operator/)


## 1. Requirements

To run Jenkins Operator, you will need:

- access to a **Kubernetes** cluster version **1.11+**
- **kubectl** version **1.11+**


## 2. Configure Custom Resource Definition

The Custom Resource Definition (CRD) API has been introduced to Kubernetes in v1.7 and it enables users to add custom APIs to their Kubernetes cluster which can be used like any other native Kubernetes objects. Defining a CRD object creates a new custom resource with a name and schema that you specify. The Kubernetes API serves and handles the storage of your custom resource.

Install Jenkins Custom Resource Definition:

    kubectl -n jenkins apply -f jenkins-crd/jenkins_v1alpha2_jenkins_crd.yaml


## 3. Deploy Jenkins Operator Using YAML’s

Create a namespace for the operator:

    kubectl create namespace jenkins

Apply Service Account and RBAC roles (Jenkins Operator):

    kubectl -n jenkins apply -f jenkins-operator/all-in-one-v1alpha2.yaml

Watch Jenkins Operator instance being created:

    kubectl -n jenkins get pods -w



## 4. Add some initial jenkins configurations (ConfigMap)
    
Configure jenkins instance adding a ConfigMap to change the layout and add new users, among others things:

    kubectl -n jenkins apply -f user-configurations/jenkins-operator-user-configuration.yaml


## 5. Add kubernetes Secrets

Usernames and their passwords, as also slack chat access:

    kubectl -n jenkins apply -f users_accounts/jenkins-conf-secrets.yaml


## 6. Create PVC

Run the following command to create a new volume to store backup data:

    kubectl -n jenkins create -f pvc.yaml

## 7. Deploy Jenkins Instance

Once Jenkins Operator is up and running let’s deploy the Jenkins instance:

    kubectl -n jenkins create -f jenkins_instance.yaml



