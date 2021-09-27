# Mailchimp&reg; Open Commerce packaged by DemandCluster

[Open Commerce](https://mailchimp.com/developer/open-commerce/) An open source, API-first, modular commerce stack made for technical, growth-minded retailers.

Disclaimer: The respective trademarks mentioned in the offering are owned by the respective companies. We do not provide a commercial license for any of these products. This listing has an open-source license. Open Commerce is run and maintained by Mailchimp, which is a completely separate project from DemandCluster.
The Helm chart is based on https://github.com/merchstack/reaction-oss-helm-chart

## TL;DR

```bash
$ helm repo add demandcluster https://demandcluster.github.io/helm-charts/
$ helm install opencommerce demandcluster/opencommerce
```

## Introduction

This chart bootstraps a [Open Commerce](https://mailchimp.com/developer/open-commerce/) deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

## Prerequisites

- Kubernetes 1.12+
- Helm 3.1.0
- PV provisioner support in the underlying infrastructure

## Installing the Chart

To install the chart with the release name `opencommerce`:

```bash
$ helm install opencommerce demandcluster/opencommerce
```

The command deploys Open Commerce on the Kubernetes cluster in the default configuration. The [Parameters](#parameters) section lists the parameters that can be configured during installation.

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `opencommerce` deployment:

```bash
$ helm delete opencommerce
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Parameters

WIP - Check the values.yaml file for now.
