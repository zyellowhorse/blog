---
setup: |
  import Layout from '../../layouts/BlogPost.astro'
title: Export Existing ECS Environment to Terraform
publishDate: 8 Dec 2021
name: Zac Yellowhorse
description: We used AWS copilot to create the ECS environments but now we want to move to Terraform so we can have better IaC...

---

- [The Problem](#the-problem)
- [Export](#export)
- [Terraformer Issues](#terraformer-issues)
- [Fixes](#fixes)
- [Final Thoughts](#final-thoughts)


## The Problem
We used AWS copilot to create the ECS environments but now we want to move to Terraform so we can have better IaC. AWS copilot is great for getting something stood up quickly but it was unable to support our needs going forward.

Copilot creates alot of resources for us and its good to understand exactly what it created for us. Copilot uses CloudFormation under the hood and as such it creates CloudFormation stacks at the end of the day. When wanting to export existing infrastructure to Terraform its good to look at the resources listed in the CloudFormation stack

## Export
I am going to be using the tool Terraformer to export the existing infrastructure. Terraformer works by reading through your cloud platform and turns the existing infrastructure into HCL files so you don't have to manually recreate everything. You can supply a filter to the tool so that its not going over your entire account and only looks at specific services or resources.

I setup the tool according to their documentation found [here](https://github.com/GoogleCloudPlatform/terraformer). After messing around with it for a bit I tweaked the filter to my liking so Its only looking at the resources that copilot created as well as only one environment. Here is what my command looks like
```
terraformer import aws --path-pattern="{output}/" --regions=us-east-1 --resources="*" --filter="Name=tags.copilot-environment;Value=prod:prod2"
```
I wont go into detail about what everything in there does as it can be read about on Terraformer's repository README.

Running the command exports all the resources that have the tag environment and the value equals prod or prod2.

## Terraformer Issues
While Terraformer is a great tool and gets you pretty far in creating IaC I would not say that what it produces should be directly used right away.

When it exports it setups the internal names of resources as the resource ID which is not pretty so you should update them to be something more readable.

Terraformer also uses some out dated syntax which with the new versions of Terraform have deprecated. These should also be fixed up manually.

Another thing to check is to make sure that the version of Terraform that it sets up in it local statefile is one that you would like to use. Also the provider version is correct for what you want to use.

I feel like this tool is good for "downloading" your current infrastructure then recreating rather then creating IaC around your existing infrastructure.

## Fixes
With those issues mentioned I am not going to be using the statefile that it creates. I am going to creating levels of abstraction upon the files that it created as well as put in place better practices. Things like crating modules for the networking and services / task definitions. When it comes times to run the actual Terraform I am going to be running `terraform init` to stand it up as if it was totally new.

## Final Thoughts
Overall Terraformer is a good tool but requires fixes afterwards. It was useful to get the configuration from a AWS copilot which did not have great documentation on what exactly it was creating and setup behind the scenes of the CLI tool. If I were tasked to set up this environment that was not created by copilot I would do it manually without Terraformer because it created a lot of headache to parse through everything and fix it up.s
