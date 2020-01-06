
---
layout: post
title: "Expose Prometheus Metrics for Kubernetes' Cluster-Autoscaler"
date: 2018-04-08 00:26:00
---

If you intend to leverage autoscaling on Kubernetes, you may want the [Cluster Autoscaler](https://github.com/kubernetes/autoscaler/tree/master/cluster-autoscaler) to expose some metrics for you. It's pretty simple to a) enable access to the `/metrics` route and b) instruct your Prometheus to scrape it:


a) Expose port 8085 for your Cluster Autoscaler deployment:
```
ports:
--name: app
 containerPort: 8085
```

See line 50 in [this gist](https://gist.github.com/dictvm/5af609e9b40709ca551655df31c10854) of an example deployment manifest.

b) Add the following annotation to your Cluster Autoscaler service:
```
prometheus.io/scrape: 'true'
```
See [this gist](https://gist.github.com/dictvm/5af609e9b40709ca551655df31c10854) of an example service manifest.
To get started, [this](https://grafana.com/dashboards/3831) is a pretty nice Grafana dashboard to make the exposed metrics instantly more useful for you.
If you're using [Network Policies](https://kubernetes.io/docs/concepts/services-networking/network-policies/), which you should, use [this](https://gist.github.com/dictvm/85a42c049b0ab72a38cc8ad5a921d64d) as a starting point to allow the scraper to actually connect to the exposed metrics route.

You may need to edit the namespaces, depending on your configuration.

You'll now be able to use the Cluster Autoscaler with much more confidence.

Hit me up on [Twitter](https://twitter.com/dictvm) to let me know if and how autoscaling is working out for you. Don't hesitate to contact me if you're stuck somewhere.