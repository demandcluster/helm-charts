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

`values.yaml`

```yaml
##
## Global configuration
global:
  ##
  ## The Stripe secret key from your Stripe account dashboard.
  ## Required if you want Stripe payments to work.
  stripeKey: YOUR_PRIVATE_STRIPE_API_KEY

  ##
  ## Set this if you want to track storefront analytics such as
  ## page views with Segment. You can find this key on your Segment dashboard.
  segmentKey: YOUR_PRIVATE_SEGMENT_API_KEY

  ## A secret token that you need to change
  tokenSecret: youNeedToChangeThis!
  ## The MongoDB database URL.
  ## Note: This overrides the Mongo subchart values i.e. bring your own
  # mongoUrl:

  ##
  ## The oplog URL for the MongoDB deployment.
  ## Note: This overrides the Mongo subchart values i.e. bring your own
  # mongoOplogUrl:

##
## Admin panel configuration
admin:
  enabled: true
  ssl: true
  host: admin.example.shop
  replicaCount: 1
  image:
    repository: reactioncommerce/admin
    tag: 4.0.0-beta.7
    pullPolicy: IfNotPresent
    # imagePullSecret:
  service:
    annotations: {}
    type: ClusterIP
  ingress:
    enabled: true
    path: "/"
    annotations: {}
    livenessPath:
    tls:
      enabled: false
      secretName: tls-secret

##
## API configuration
api:
  enabled: true
  host: api.example.shop
  ssl: true
  replicaCount: 1

  ##
  ## Serve the GraphQL Playground UI from /graphql
  # enableGraphQlPlayground: false

  ##
  ## Allow introspection of the GraphQL API.
  # enableGraphQlIntrospection: false

  ##
  ## An SMTP mail url, e.g. smtp://user:pass@example.com:465, that is
  ## used to send all transactional emails from the email-smtp plugin.
  # mailUrl: smtp://user:pass@example.com:465

  ##
  ## If this is true, on startup the API will auto-initialize a MongoDB
  ## replica set if one isn't found.

  initReplicaSet: true
  image:
    repository: reactioncommerce/reaction
    tag: 4.0.3
    pullPolicy: IfNotPresent
    # imagePullSecret:
  service:
    annotations: {}
    type: ClusterIP
  ingress:
    enabled: true
    path: "/"
    annotations: {}
    livenessPath:
    tls:
      enabled: false
      secretName: tls-secret

##
## Example storefront configuration
storefront:
  enabled: true
  host: example.shop
  ssl: true
  replicaCount: 1
  sessionSecret: CHANGEME
  image:
    repository: reactioncommerce/example-storefront
    tag: 5.0.3
    pullPolicy: IfNotPresent
    # imagePullSecret:
  service:
    annotations: {}
    type: ClusterIP
  ingress:
    enabled: true
    path: "/"
    annotations: {}
    livenessPath:
    tls:
      enabled: true
      secretName: tls-secret
##
## MongoDB chart configuration
mongodb:
  enabled: true
  auth:
    enabled: true
    rootPassword: reaction
    rootUser: admin
  architecture: replicaset
  replicaSetName: rs0
  replicaCount: 2
  persistence:
    enabled: true
    size: 8Gi
  arbiter:
    enabled: true
  service:
    annotations: {}
    type: ClusterIP
    port: 27017
```
