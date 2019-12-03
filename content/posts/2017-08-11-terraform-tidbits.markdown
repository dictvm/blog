---
layout: post
title: Terraform Tidbits
date: '2017-08-11 13:09:35'
---

Terraform is a pretty useful tool to manage Infrastracture as Code with various Cloud providers. However, as with any complex software, you might encounter weird issues or shortcomings. I'll try to extend this post as I continue to work with Terraform. Don't expect magic here, it's mostly just a few one-liners that might help you to get your work done more quickly.

## Taint all module resources

When you've developed a Terraform module and you want to roll it out into production it might be wise to tear down everything one last time to recreate it from scratch.

First, you cannot easily taint all resources of a module out of the box. But we can do this:

```
for i in $(terraform show -module-depth=1 | grep module.consul-cluster | tr -d ':' | sed -e 's/module.consul-cluster.//'); do terraForm taint -module consul-cluster $i; done
```

Simpler, with less redundancy:

```
export TF_MODULE=consul-cluster

for i in $(terraform show -module-depth=1 | grep module.$TF_MODULE | tr -d ':' | sed -e 's/module.$TF_MODULE.//'); do terraForm taint -module $TF_MODULE $i; done
```

## Race condition during deletion/creation of IAM resources

Terraform sometimes seems to stumble during the recreation of IAM instance profiles, especially when there are are policies and roles attached to it when using AWS as your provider.

The error message reads as follows:

```
EntityAlreadyExists: Instance Profile $your_instance_profile already exists.
```

It helps to just delete the instance profile manually using the cli:

`aws iam delete-instance-profile --instance-profile-name $your_instance_profile`

Terraform should now be able to recreate all tainted resources.

That's it for now.
