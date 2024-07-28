# Terraform Load Balancer Module

This Terraform module allows you to easily create a load balancer in your infrastructure.

## Features

- Supports both Application Load Balancer (ALB) and Network Load Balancer (NLB)
- Configurable listeners and target groups
- Automatic scaling based on CloudWatch metrics
- Integration with other AWS services like Auto Scaling Groups and ECS

## Usage

```hcl
module "load_balancer" {
    source = "github.com/your-username/load-balancer"

    name        = "my-load-balancer"
    environment = "production"
    vpc_id      = "vpc-12345678"

    listeners = [
        {
            port     = 80
            protocol = "HTTP"
        },
        {
            port     = 443
            protocol = "HTTPS"
            certificate_arn = "arn:aws:acm:us-west-2:123456789012:certificate/abcdefg"
        }
    ]

    target_groups = [
        {
            name     = "web-servers"
            protocol = "HTTP"
            port     = 80
        },
        {
            name     = "api-servers"
            protocol = "HTTP"
            port     = 8080
        }
    ]
}
```

## Inputs

| Name         | Description           | Type   | Default | Required |
|--------------|-----------------------|--------|---------|----------|
| name         | The name of the load balancer | string | n/a | yes |
| environment  | The environment in which the load balancer is deployed | string | n/a | yes |
| vpc_id       | The ID of the VPC where the load balancer will be created | string | n/a | yes |
| listeners    | A list of listener configurations for the load balancer | list(object) | n/a | yes |
| target_groups | A list of target group configurations for the load balancer | list(object) | n/a | yes |

## Outputs

| Name         | Description           |
|--------------|-----------------------|
| load_balancer_arn | The ARN of the load balancer |
| load_balancer_dns_name | The DNS name of the load balancer |
| target_group_arns | The ARNs of the target groups |
