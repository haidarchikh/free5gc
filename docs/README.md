# towards5GS-helm documentation

Welcome to the **towards5GS-helm** documentation main page!

## Prerequisites

Before going to use our Helm charts, you have to:

### Create a Kubernetes cluster
The are many solutions for the creation of a Kubernetes cluster. Feel free to visit this [page](https://kubernetes.io/fr/docs/setup/pick-right-solution/) to discover a part of these solutions.
If you don't dispose yet of a Kubernetes cluster, we recommend you to use [Kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/) regarding to its simplicity.

### Install Helm
You have to install a Helm client on a host that can communicate with your Kubernetes API server. 
```console
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
```
Refer to this [link](https://helm.sh/docs/intro/install/) to view all possible installation methods.

## Using our Helm charts

### Using edge versions
```console
git clone https://github.com/raoufkh/5gprojects.git
```
The edge versions of all charts are available on the [charts](../charts/) directory.

### Using stable versions
The stable versions of all charts are available on the [towards5GS repository](../repo/).
```console
helm repo add towards5gs 'https://raw.githubusercontent.com/raoufkh/5gprojects/master/repo/'
helm repo update
helm search repo
```
If you want to install a specific version from a specific chart run:
```console
helm install {replace by the name of the chart} --version --version {replace by the version of the chart}
```
If you want to download its packaged archive to your local directory run:
```console
helm pull {replace by the name of the chart} --version --version {replace by the version of the chart}
```

## Setup methods
In addition to the README provided in each Helm chart, the [Documentation](.) directory provides several guidelines for different implementations:
 - [Setup free5gc on multiple clusters and test with UERANSIM](./Setup-free5gc-on-multiple-clusters-and-test-with-UERANSIM.md)
 - [Setup free5gc on multiple clusters with a Kubernetes service to expose the AMF NGAP service and test with UERANSIM](./Setup-free5gc-with-a-Kubernetes-service-to-expose-the-AMF-NGAP-service-and-test-with-UERANSIM.md)
 - [Setup free5gc on multiple clusters with ULCL mode and test with UERANSIM](./Setup-free5gc-on-multiple-clusters-with-ULCL-mode-and-test-with-UERANSIM.md)




