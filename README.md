# ECS Singleton Task

**This module assumes an EC2 launch type.** For the complimentary fargate task, [go here.](https://github.com/7Factor/terraform-fargate-ecs-singleton-task)

This module will allow you to deploy an ECS Task and an ECS Service. This is intended to be run as part of your app deployment
pipeline. It works well with [Concourse.](https://concourse-ci.org) It is assumed you already have a solution for deploying an
ECS Cluster. If not, check out [ours](https://github.com/7Factor/terraform-ecs-cluster).

This is a bare metal service implementation with no load balancers, target groups, and the like. If you want to deploy something
with a load balancer you should check out our [HTTP](https://github.com/7Factor/terraform-ecs-http-task) task.

## Prerequisites

First, you need a decent understanding of how to use Terraform. [Hit the docs](https://www.terraform.io/intro/index.html) for that.
Then, you should familiarize yourself with ECS [concepts](https://aws.amazon.com/ecs/getting-started/), especially if you've
never worked with a clustering solution before. Once you're good, import this module and  pass the appropriate variables.
Then, plan your run and deploy.

## Example Usage

```hcl-terraform
module "terraform-ecs-task" {
  source                = "git::https://github.com/7Factor/terraform-ecs-singleton-task.git"
  vpc_id                = "${data.aws_vpc.primary_vpc.id}"

  app_name              = "${var.app_name}"
  cpu                   = "256"
  memory                = "256"
  desired_task_count    = "2"
  container_definition = "${data.template_file.container_definitions.rendered}"
}
```
