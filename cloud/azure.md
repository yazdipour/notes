# Getting Started with AKS

## Run Azure CLI

```
docker run -it --rm -v ${PWD}:/work -w /work --entrypoint /bin/sh mcr.microsoft.com/azure-cli
```

## Login to Azure

```
#login and follow prompts
az login

# view and select your subscription account

az account list -o table
SUBSCRIPTION=<id>
az account set --subscription <SubscriptionId-id-here>
```

## Create our Resource Group

```
RESOURCEGROUP=aks-getting-started
az group create -n $RESOURCEGROUP -l australiaeast

```

## Create Service Principal

Kubernetes needs a service account to manage our Kubernetes cluster </br>
Lets create one! </br>

```sh
SERVICE_PRINCIPAL_JSON=$(az ad sp create-for-rbac --skip-assignment --name aks-getting-started-sp -o json)

#Keep the `appId` and `password` for later use!

SERVICE_PRINCIPAL=$(echo $SERVICE_PRINCIPAL_JSON | jq -r '.appId')
SERVICE_PRINCIPAL_SECRET=$(echo $SERVICE_PRINCIPAL_JSON | jq -r '.password')

#grant contributor role over the resource group to our service principal

az role assignment create --assignee $SERVICE_PRINCIPAL \
--scope "/subscriptions/$SUBSCRIPTION/resourceGroups/$RESOURCEGROUP" \
--role Contributor
```

For extra reference you can also take a look at the Microsoft Docs: [here](https://github.com/MicrosoftDocs/azure-docs/blob/master/articles/aks/kubernetes-service-principal.md) </br>

## Create our cluster

```sh
#full list of options

az aks create --help
az aks get-versions --location australiaeast -o table

#generate SSH key

ssh-keygen -t rsa -b 4096 -N "VeryStrongSecret123!" -C "your_email@example.com" -q -f  ~/.ssh/id_rsa
cp ~/.ssh/id_rsa* .

az aks create -n aks-getting-started \
--resource-group $RESOURCEGROUP \
--location australiaeast \
--kubernetes-version 1.16.10 \
--load-balancer-sku standard \
--nodepool-name default \
--node-count 1 \
--node-vm-size Standard_E4s_v3  \
--node-osdisk-size 250 \
--ssh-key-value ./id_rsa.pub \
--network-plugin kubenet \
--service-principal $SERVICE_PRINCIPAL \
--client-secret $SERVICE_PRINCIPAL_SECRET \
--output none

# if your SP key is invalid, generate a new one:
SERVICE_PRINCIPAL_SECRET=(az ad sp credential reset --name $SERVICE_PRINCIPAL | jq -r '.password')
```

## Get a kubeconfig for our cluster

```
# use --admin for admin credentials
# use without `--admin` to get no priviledged user.

az aks get-credentials -n aks-getting-started \
--resource-group $RESOURCEGROUP

#grab the config if you want it
cp ~/.kube/config .

```

## Get kubectl

```
curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl
chmod +x ./kubectl
mv ./kubectl /usr/local/bin/kubectl

cd ../..

kubectl create ns example-app

# lets create some resources.
kubectl apply -n example-app -f secrets/secret.yaml
kubectl apply -n example-app -f configmaps/configmap.yaml
kubectl apply -n example-app -f deployments/deployment.yaml

# remember to change the `type: LoadBalancer`
kubectl apply -n example-app -f services/service.yaml

```

## Clean up

```sh
az group delete -n $RESOURCEGROUP
az ad sp delete --id $SERVICE_PRINCIPAL
```

## Start the Kubernetes dashboard

`az aks browse --resource-group myResourceGroup --name myAKSCluster`

### Signin

Set the admin kubeconfig with `az aks get-credentials -a --resource-group <RG_NAME> --name <CLUSTER_NAME>`

### Create an AKS cluster with ACR integration

`az aks create -n myAKSCluster -g myResourceGroup --generate-ssh-keys --attach-acr myACRName`

## Terraform

Providers: https://www.terraform.io/docs/providers/index.html

https://github.com/HoussemDellai/Terraform-Demo/blob/master/app-service-variables/main.tf

```sh
terraform init
terraform plan # create an executable plan
terraform apply -auto-approve #execute the plan
terraform detroy #destroy the resources /infrastructure

terraform refresh #query infrastructure provider to get current state
```

## Helm

https://github.com/helm/charts/tree/master/stable
https://www.youtube.com/watch?v=DczwTQE5T2M

```sh
helm create x
helm package x
helm install x //to deply to kub
```

## Kub Service SSL

https://docs.microsoft.com/en-us/azure/application-gateway/ingress-controller-expose-service-over-http-https

https://www.youtube.com/watch?v=5S_395VKMqs
1 https://cert-manager.io/docs/installation/kubernetes/

2 https://cert-manager.io/docs/concepts/issuer/

helm install cert-manager jetstack/cert-manager --namespace cert-manager --version v1.0.4 --set installCRDs=true
