Terraform module for Kubernetes Ingress
==========================================

## Usage (more in example direcotry)

With default labels, selector finds pods with `app` label which equal to `app_name`

### Example with ClusterIP
```
module "ingress" {
  source = "../"
  
  app_name      = module.service.name
  app_namespace = var.namespace
  annotations   = {
    "kubernetes.io/ingress.class" = "nginx-custom" // Default: nginx
  }

  web_internal_port = [
    {
      domain        = local.url
      internal_port = var.ports_mapping.0.internal_port // Service port
    }
  ]
  tls_hosts = [
    {
      secret_name = "cert-manager-ingress"
      hosts       = [example.com]
    }
  ]
}
```


## Terraform Requirements

| Name | Version |
|------|---------|
| terraform | >= 0.12.26 |
| kubernetes | >= 1.12.0 |

## Inputs
See in example directory & variables.tf

## Outputs
| Name | Description |
|------|:-----------:|
| id | Kubernetes resource id |
| urls | URLs in ingress |
| load_balancer_ingress_ip | IP is set for load-balancer ingress points that are IP based |
| load_balancer_ingress_hostname | Hostname is set for load-balancer ingress points that are DNS based |