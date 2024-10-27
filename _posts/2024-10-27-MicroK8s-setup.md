---
layout: post
title: Ubuntu Microk8s Setup
date: '2024-10-28T16:40:00.000-08:00'
author: MaX
tags:
- Kubern8s
- DevOps
- Development
- Containers
- Cloud
modified_time: '2024-10-28T16:40:00.000-08:00'
thumbnail: /img/in-post/covid_graph.png
---
# Setup Microk8s
Few steps to setup MicroK8s on Ubuntu linux... and start to use it quickly...

## Install MicroK8s on Linux

sudo snap install microk8s --classic

## Check the status while Kubernetes starts

microk8s status --wait-ready

## Turn on the services you want

microk8s enable dashboard
microk8s enable dns
microk8s enable registry
microk8s enable istio
Try microk8s enable --help for a list of available services and optional features. microk8s disable <name> turns off a service.

## Start using Kubernetes

microk8s kubectl get all --all-namespaces
If you mainly use MicroK8s you can make our kubectl the default one on your command-line with alias mkctl="microk8s kubectl". Since it is a standard upstream kubectl, you can also drive other Kubernetes clusters with it by pointing to the respective kubeconfig file via the --kubeconfig argument.

## Access the Kubernetes dashboard

microk8s dashboard-proxy

Create a Tocken and copy it...
microk8s kubectl create token default

Creat port forwarding:
microk8s kubectl port-forward -n kube-system service/kubernetes-dashboard 10443:443

You can then access the Dashboard at https://127.0.0.1:10443.