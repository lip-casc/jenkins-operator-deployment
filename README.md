# Jenkins
All informations can be found at [https://jenkinsci.github.io/kubernetes-operator/](https://jenkinsci.github.io/kubernetes-operator/)


#### Create the namespace for jenkins-operator and jenkins instance:
    kubectl create ns jenkins-operator
    kubectl create ns jenkins

#### Create necessary resources in Jenkins Operator namespace:
    kubectl apply -f jenkins-operator-crd.yaml
    kubectl apply -n jenkins-operator -f jenkins-operator-rbac.yaml
    kubectl apply -n jenkins-operator -f jenkins-operator.yaml