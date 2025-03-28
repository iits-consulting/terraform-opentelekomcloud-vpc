# Module to auto create VPC and multiple Subnet

Usage example

```hcl
module "vpc" {
  source     = "iits-consulting/vpc/opentelekomcloud"

  name       = "vpc-demo-${local.stage_name}"
  cidr_block = "10.0.0.0/16"
  subnets = {
    "kubernetes-subnet" = cidrsubnet(var.cidr_block, 2, 0)
    "database-subnet"   = cidrsubnet(var.cidr_block, 3, 2)
    "jumphost-subnet"   = cidrsubnet(var.cidr_block, 3, 3)
  }
}
```

> **WARNING:** using defaults for `cidr_block` and `subnets` is not recommended!
>
> These parameters define network address ranges (CIDR) and must be chosen based on requirements.
> Changing them at a future point will cause the network to be recreated, destroying any resource within!

<!-- BEGIN_TF_DOCS -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 1.5.7 |
| <a name="requirement_opentelekomcloud"></a> [opentelekomcloud](#requirement\_opentelekomcloud) | ~> 1.32 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_opentelekomcloud"></a> [opentelekomcloud](#provider\_opentelekomcloud) | ~> 1.32 |

## Modules

No modules.

## Resources

| Name | Type |
|------|------|
| [opentelekomcloud_vpc_subnet_v1.subnets](https://registry.terraform.io/providers/opentelekomcloud/opentelekomcloud/latest/docs/resources/vpc_subnet_v1) | resource |
| [opentelekomcloud_vpc_v1.vpc](https://registry.terraform.io/providers/opentelekomcloud/opentelekomcloud/latest/docs/resources/vpc_v1) | resource |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_name"></a> [name](#input\_name) | Name of the VPC. | `string` | n/a | yes |
| <a name="input_cidr_block"></a> [cidr\_block](#input\_cidr\_block) | IP range of the VPC | `string` | `"10.0.0.0/16"` | no |
| <a name="input_dns_config"></a> [dns\_config](#input\_dns\_config) | Common Domain Name Server list for all subnets | `list(string)` | <pre>[<br/>  "100.125.4.25",<br/>  "100.125.129.199"<br/>]</pre> | no |
| <a name="input_subnets"></a> [subnets](#input\_subnets) | Subnet names and their cidr ranges. | `map(string)` | <pre>{<br/>  "database-subnet": "",<br/>  "jumphost-subnet": "",<br/>  "kubernetes-subnet": ""<br/>}</pre> | no |
| <a name="input_tags"></a> [tags](#input\_tags) | Common tag set for project resources | `map(string)` | `{}` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_subnets"></a> [subnets](#output\_subnets) | n/a |
| <a name="output_vpc"></a> [vpc](#output\_vpc) | n/a |
<!-- END_TF_DOCS -->
