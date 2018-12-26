AWS VPC Peering Connection Module
=================================

Terraform module, which creates a peering connection between two VPCs and adds routes to the local VPC.

Usage
-----

### Single Region Peering
**Notice**: You need to declare both providers even with single region peering.

```hc1
module "vpc_single_region_peering" {
  source = "./terraform-aws-vpc-peering"

  providers = {
    aws.this = "aws"
    aws.peer = "aws"
  }

  peer_region             = "eu-west-1"
  this_vpc_id             = "vpc-aaaaaaaa"
  peer_vpc_id             = "vpc-bbbbbbbb"
  cross_region_peering    = false
  auto_accept_peering     = true
  create_peering          = true

  tags = {
    Name        = "my-peering-connection"
    Environment = "prod"
  }
}
```

Usage with already created peering connection:
```hc1 
module "vpc_single_region_peering" {
  source = "./terraform-aws-vpc-peering"

  providers = {
    aws.this = "aws"
    aws.peer = "aws"
  }

  peer_region             = "eu-west-1"
  this_vpc_id             = "vpc-aaaaaaaa"
  peer_vpc_id             = "vpc-bbbbbbbb"
  cross_region_peering    = false
  auto_accept_peering     = true
  create_peering          = 0
  peering_id              = "pcx-aaaaaaaa"

}
```

### Cross Region Peering

```hc1
module "vpc_cross_region_peering" {
  source = "./terraform-aws-vpc-peering"

  providers = {
    aws.this = "aws.src"
    aws.peer = "aws.dst"
  }

  peer_region             = "us-east-1"
  this_vpc_id             = "vpc-aaaaaaaa"
  peer_vpc_id             = "vpc-bbbbbbbb"
  cross_region_peering    = true
  auto_accept_peering     = true
  create_peering          = true

  tags = {
    Name        = "my-peering-connection"
    Environment = "prod"
  }
}
```

License
-------
Apache 2 Licensed. See LICENSE for full details.
