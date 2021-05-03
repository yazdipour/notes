# Terraform

https://docs.microsoft.com/en-us/azure/developer/terraform/create-k8s-cluster-with-tf-and-aks?toc=https%3A%2F%2Fdocs.microsoft.com%2Fen-us%2Fazure%2Faks%2Ftoc.json&bc=https%3A%2F%2Fdocs.microsoft.com%2Fen-us%2Fazure%2Fbread%2Ftoc.json

Providers: https://www.terraform.io/docs/providers/index.html

https://github.com/HoussemDellai/Terraform-Demo/blob/master/app-service-variables/main.tf

```sh
terraform init
terraform plan # create an executable plan
terraform apply -auto-approve #execute the plan
terraform detroy #destroy the resources /infrastructure

terraform refresh #query infrastructure provider to get current state
terraform state list
terraform state show x
```
