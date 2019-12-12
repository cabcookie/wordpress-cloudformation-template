# A CloudFormation template to create a Wordpress blog, reliable and scalable

Build status: experimentation

## Purpose of this repo

This repos purpose is to provide a CloudFormation template which creates an infrastructure in AWS to run a Wordpress blog on it. The idea is to set all parameters in the master file, then run the master file and everything else happens automatically.

The repo is organized with nested templates. Those templates are being pointed to on GitHub itself and are as stable as possible.

## Prerequisites

The template is there to create the infrastructure but the following prerequisites need to be fulfilled manually:

1. Create an S3 bucket with `aws s3 mb s3://<bucket name>` and copy the templates folder into this bucket with `aws s3 cp templates s3://<bucket name> --recursive`
2. Create security key pair in the EC2 console and download it (the name is used in the parameter `KeyPairName`)
3. Create an ACM Certificate for the CloudFront distribution in the us-east-1 region (the ARN is used in the parameter `CertificateARNCloudFront`)
4. Create an ACM Certificate for the Elastic Loadbalancer in the region where the Wordpress installation is hosted or re-use #2 if it's the same region (the ARN is used in the parameter `CertificateARNLoadBalancer`)

TODO: Explain how to validate ownership of the domain

## Run the master template

Start building the infrastructure with the following AWS CLI statement within the folder of the `master.yaml` file:

    aws cloudformation create-stack --stack-name master --template-body file://master.yaml --capabilities CAPABILITY_IAM

## Mandatory parameters

### Settings for templates

* `TemplateBucket`: S3 Bucket where to find the templates for CloudFormation

### Settings for networking

* `Domain`: domain to be used for the Wordpress blog
* `CertificateARNCloudFront`: The ARN for the certificate used for CloudFront
* `CertificateARNLoadBalancer`: The ARN for the certificate used for Elastic Load Balancer

### Settings for EC2 instances

No mandatory settings.

### Settings for alarming & notifications

No mandatory settings.

## Optional parameters

### Settings for templates

No optional parameters.

### Settings for networking

* `SubdomainWordpress`: subdomain being used for the Wordpress page (default `blog` results into **blog**.domain.com)
* `ClassBIP`: Class B of VPC (10.XXX.0.0/16) (default `0`)

### Settings for EC2 instances

* `KeyPairName`: Name of the security key pair generated in the EC2 console (default `Wordpress`)

### Settings for alarming & notifications

* `Email`: Email adress for notifications or alarms
* `Phone`: Phone number for notifications or alarms
