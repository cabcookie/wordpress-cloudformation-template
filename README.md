# A CloudFormation template to create a Wordpress blog, reliable and scalable

Build status: experimentation

## Purpose of this repo

This repos purpose is to provide a CloudFormation template which creates an infrastructure in AWS to run a Wordpress blog on it. The idea is to set all parameters in the master file, then run the master file and everything else happens automatically.
The repo is organized with nested templates. Those templates are being pointed to on GitHub itself and are as stable as possible.

## Prerequisites

The template is there to create the infrastructure but it will not create a domain name, relate it to a region and it will not create security key pairs. That is something that needs to be created manually beforehand. Follow these steps:

1. Go to the EC2 console and create a key pair. Download the key pair. You will need the name of your key pair later in the master file (or just name it Wordpress to use the default name).
2. Create a domain name for your Wordpress blog with the registrar of your choice (AWS is also a registrar).
3. Go to the Certificate Manager console and create a certificate (or one per purpose) that is to be used for (a) connecting the Bastion host (admin access) from where we connect to other hosts or databases (use `ssh` as a default), (b) connecting the web server to show the page (public access, use `www` as a default). The Certificate Manager asks you to validate the URLs by adding CNAME texts at your domain provider. If you used AWS as your registrar you can just add the texts into Route53 by clicking the buttons shown with the config.

## Settings in master file

TODO: Define settings
