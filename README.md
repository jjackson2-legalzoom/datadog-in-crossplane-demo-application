# datadog-in-crossplane-demo-application

## Rough notes for presentation

* First off - this is _not_ how we should be managing these resources. We already have the [DataDog Operator](https://docs.datadoghq.com/getting_started/containers/datadog_operator/) installed, which allows the creation of Datadog resources _directly_ from k8s manifests ([e.g.](https://github.legalzoom.com/engineering/authorization-service-deployment/blob/master/envs/prd/monitoring.yaml)). At that point, the key advantage of Crossplane ("_it lets you use Kubernetes as a Control Plane for non-k8s-native resources_") disappears. It _does_ provide some useful functionality in that it allows "bundling" of resources (i.e. defining one high-level parameterizable resource which is translate to many lower-level ones) - but cdk8s also does that, and does it better (in code rather than config), so in fact I advise:
  * For any resources which are natively supported in k8s: `cdk8s` alone ("creation" is managed by k8s itself)
  * For other resources: `cdk8s` for definition and Crossplane for creation.