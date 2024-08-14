# ExternalDNS for Kubernetes using AWS with a Trust Policy

ExternalDNS is a Kubernetes addon that allows you to automatically create DNS records in Route 53 for your Kubernetes services and ingresses. This is especially useful if you are running your Kubernetes cluster on AWS and using Route53 for DNS.

This repository provides a Kubernetes manifest file for running External DNS with Route53 on your cluster.

## ExternalDNS Architecture and Background:

### Introduction

ExternalDNS is a Kubernetes controller that automates the management of DNS records for Kubernetes resources. ExternalDNS uses the Kubernetes API to discover services and ingresses that need DNS records, and then updates the DNS provider accordingly. This makes it easy to manage DNS records for Kubernetes resources, especially in environments where DNS management is a manual process.

## Architecture

ExternalDNS has a simple architecture that consists of two main components: the ExternalDNS controller and the DNS provider. The ExternalDNS controller runs as a Kubernetes deployment, and its main responsibility is to discover services and ingresses that need DNS records. The DNS provider is responsible for actually managing the DNS records.

The ExternalDNS controller watches the Kubernetes API for changes to services and ingresses that need DNS records. When a change is detected, the controller updates the DNS provider with the appropriate DNS records. The DNS provider can be a variety of DNS providers, including AWS Route53, Google Cloud DNS, and others.

## Background:

Managing DNS records for Kubernetes resources can be a tedious and error-prone process, especially in environments where DNS management is a manual process. ExternalDNS was created to automate this process and make it easier to manage DNS records for Kubernetes resources.

## Conclusion:

ExternalDNS is a useful tool for managing DNS records for Kubernetes resources. It automates the process of discovering services and ingresses that need DNS records and updates the DNS provider accordingly. With ExternalDNS, you can easily manage DNS records for Kubernetes resources in environments where DNS management is a manual process.

## Prerequisites:

Before installing ExternalDNS, you'll need:
-- A Kubernetes cluster running version 1.10 or higher
-- `kubectl` CLI installed
-- An AWS account with Route 53 access
-- An IAM policy and role that allows ExternalDNS to manage Route 53 DNS records

**Note:** It's important to note that when implementing a policy for Amazon Route 53, it may be beneficial to limit the policy to a specific Route 53 Zone ID in order to isolate the policy and prevent unintended consequences. This can help to ensure that the policy only applies to the specific resources in the designated zone and not to other resources in the account.

## Usage:

Once you've installed ExternalDNS, it will automatically create Route 53 DNS records for any Kubernetes services and ingresses with the `external-dns.alpha.kubernetes.io/hostname` annotation. 

## Cleanup:

To stop using ExternalDNS and clean up your Kubernetes cluster, you can run the following commands:

**Option A**

To delete the ExternalDNS resources, you would run `make stop`, and to completely destroy the namespace, along with anything within that namespace, you would run `make destroy`.

**Option B**

```bash 
kubectl delete -f externaldns.yaml
kubectl delete namespace externaldns
```

## Debugging:

I began by gaining an overview of the project requirements and breaking them down into smaller tasks. 

- I highly recommend creating a plan before diving into a project - it helps to clarify your goals and make the overall task feel more manageable.

**Typos:** Making typos in YAML files can cause significant issues and can be time-consuming to debug. I found myself making careless mistakes when putting together my deployment file. 

- Take regular breaks. This can help you avoid fatigue and reduce the likelihood of making mistakes.

**Validate your YAML files:** Before using a YAML file, validate it using a tool like `YAMLLint`. This can help you catch syntax errors and other mistakes before they cause issues.

**Don't get ahead of yourself:** Take time to stop and test certain aspects of your code before spending hours on the project only to find out that you have a bunch of errors, *like I did*. 

## Library:

1) [ExternalDNS GitHub repository](https://github.com/kubernetes-sigs/external-dns)
2) [ExternalDNS documentation](https://github.com/kubernetes-sigs/external-dns/blob/master/README.md)
3) [YAMLLint](https://www.yamllint.com/)
