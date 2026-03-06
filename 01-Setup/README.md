## Setup

Set up a kubernetes cluster
   - In a cloud platform of choice like [Amazon EKS](https://aws.amazon.com/eks), 
     [Google Kubernetes Engine](https://cloud.google.com/kubernetes-engine), 
     and [Azure Kubernetes Service](https://azure.microsoft.com/en-us/services/kubernetes-service/) OR
   - In local environment using [Minikube](https://minikube.sigs.k8s.io/docs/). 
     Note, more than 7GB of RAM is required to run Datahub and it's dependencies 

Install the following tools: 
   - [kubectl](https://kubernetes.io/docs/tasks/tools/) to manage kubernetes resources
   - [helm](https://helm.sh/docs/intro/install/) to deploy the resources based on helm charts. 
     Note, we only support Helm 3

Create a new namespace in a Kubernetes cluster

```sh
kubectl create namespace datath-datahub-1
```

<img src="image\kubectl create namespace datath-datahub-1.png" width=100% height=40%>

Add datahub helm repo by running the following

```sh
helm repo add datahub https://helm.datahubproject.io/
```

<img src="image\helm repo add datahub httpshelm.datahubprojectio.png" width=100% height=40%>

Fetch and update the latest chart index from the DataHub repository to your local system

```sh
helm repo update datahub
```

<img src="image\helm repo update datahub.png" width=100% height=40%>

Navigate to the directory where the files are stored

```sh
cd [path]
```

Example:

```sh
cd /Users/tummarakya/01_NocNoc_DE_Repo/dp-helm/datath-prereq
```

<img src="image\cd [path].png" width=100% height=40%>

Create kubernetes secrets that contain MySQL and Neo4j passwords. 

In kubernetes, a secret must be in the same namespace as the pod that uses it; if DataHub or MySQL runs in datath-datahub-1 but the secret is created in default, the Pod will not be able to access it

```(shell)
kubectl create secret generic mysql-secrets --from-literal=mysql-root-password=datahub --namespace datath-datahub-1

kubectl create secret generic neo4j-secrets --from-literal=neo4j-password=datahub --namespace datath-datahub-1 
```

The above commands sets the passwords to "datahub" as an example. Change to any password of choice

<img src="image\create kubernetes secrets.png" width=100% height=40%>
<img src="image\secret.png" width=100% height=40%>

Deploy the infrastructure/dependencies (prerequisites) before installing dataHub

```sh
helm install prerequisites /Users/tummarakya/01_NocNoc_DE_Repo/dp-helm/datath-prereq --namespace datath-datahub-1 -f values.yaml
```

<img src="image\helm install prerequisites.png" width=100% height=40%>

Navigate to the directory where the files are stored

```sh
cd [path]
```

Example:

```sh
cd /Users/tummarakya/01_NocNoc_DE_Repo/dp-helm/datath-datahub
```

<img src="image\cd [path2].png" width=100% height=40%>


Download and build the dependencies of a Helm chart

```sh
helm dependency build
```

<img src="image\helm dependency build.png" width=100% height=40%>

Deploy the dataHub application on kubernetes

```sh
helm install datahub /Users/tummarakya/01_NocNoc_DE_Repo/dp-helm/datath-datahub --namespace datath-datahub-1 -f values.yaml
```

<img src="image\helm install datahub.png" width=100% height=40%>
<img src="image\k8s.png" width=100% height=40%>

DataHub

<img src="image\DataHub.png" width=100% height=40%>