![scayle-logo-cr](https://cdn-prod.scayle.com/public/media/general/SCAYLE-Commerce-Engine-header.png)

<h1 align="center">
  SCAYLE Storefront ECS Fargate Deployment
</h1>

<h4 align="center">
  <a href="https://new.scayle.dev">Documentation</a> |
  <a href="https://www.scayle.com/">Website</a>
</h4>

<p align="center">
  This repository contains an AWS CloudFormation template to deploy the SCAYLE Storefront application on Amazon ECS using Fargate. The deployment includes an ECS cluster, task definitions, services, a load balancer, ElastiCache, IAM roles, and auto-scaling configurations.
</p>
<p align="center">
  <a href="#"><img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="SCAYLE's **Storefront API PHP SDK is released under the MIT license." /></a>
</p>

## Prerequisites

Before deploying the template, ensure you have:

1. **AWS CLI**: Installed and configured with appropriate permissions.
2. **CloudFormation**: Basic understanding of AWS CloudFormation.
3. **VPC and Subnets**: Pre-existing VPC and Subnets (public and private) where resources will be deployed.

## Parameters

### Environment

- **Environment**: Specifies the environment to deploy (dev, staging, prod).
    - Type: String
    - Default: dev
    - Allowed Values: dev, staging, prod

- **ScayleTenantSpace**: SCAYLE tenant space your storefront should connect to, e.g., acme-live.
    - Type: String
    - Allowed Pattern: `^[a-z]+(-[a-z]+)*$`

### ECS Configuration

- **Image**: Docker image to deploy.
    - Type: String
    - Default: `scayle/storefront-boilerplate:1.0.0-storyblok`

### SCAYLE Authentication

- **ScayleAuthClientId**: Your Client ID for the Authentication API from SCAYLE.
    - Type: String
    - NoEcho: true

- **ScayleAuthClientSecret**: Your Secret for the Authentication API from SCAYLE.
    - Type: String
    - NoEcho: true

- **ScayleCheckoutSecret**: Your Checkout Secret for your SCAYLE Shop.
    - Type: String
    - NoEcho: true

- **ScayleCheckoutToken**: Your Checkout Token for your SCAYLE Shop.
    - Type: String
    - NoEcho: true

- **ScayleStorefrontAPIToken**: Your Token for the Storefront API from SCAYLE.
    - Type: String
    - NoEcho: true

- **StoryblokAccessToken**: Your Storyblok Access Token for your CMS integration.
    - Type: String
    - NoEcho: true

### Network Configuration

- **PrivateSubnets**: Subnets for Service and ElastiCache.
    - Type: List<AWS::EC2::Subnet::Id>

- **PublicSubnets**: Subnets for the Load Balancer.
    - Type: List<AWS::EC2::Subnet::Id>

- **VPC**: VPC for deploying the ECS cluster.
    - Type: AWS::EC2::VPC::Id