---
tags: 
 - aws
 - eks
 - lab
generated: true
---
# aws.lab.eks

## Resources:

### EKS CLuster
https://github.com/stacksimplify/terraform-on-aws-eks
### Prometheus Operator
https://github.com/antonputra/tutorials/tree/main/lessons/154

## Implementation
### Create EKS Cluster
1. plan and apply terraform in `01-ekscluster-terraform-manifests`
2. plan and apply terraforn in `02-ebs-terraform-manifests`
3. create kubeconfig: `aws eks update-kubeconfig --region <region>  --name <cluster_id>
### Install Prometheus Operator
https://github.com/prometheus-operator/prometheus-operator
1. Create namespace
      `kubectl apply -f 03-prometheus-operator/prometheus-operator/namespace.yaml`
2. Create Prometheus CRDs
      `kubectl apply --server-side -f 03-prometheus-operator/prometheus-operator/crds`
3. Create RBAC Policies
      `kubectl apply -f 03-prometheus-operator/prometheus-operator/rbac/cluster-roles.yaml`
4. Apply deployment manifests
      `kubectl apply -f 03-prometheus-operator/prometheus-operator/deployment`

### Deploy Prometheus
1. Apply prometheus manifests
      `kubectl apply -f 03-prometheus-operator/prometheus
A service is created.
`kubectl get svc -n monitoring`

```
NAME                  TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)    AGE
prometheus-operated   ClusterIP   None         <none>        9090/TCP   11m
```

port-forward or configure ingress to this service:
`kubectl -n monitoring port-forward svc/prometheus-operated 9090`

### Deploy Sample App
`kubectl apply -f 03-prometheus-operator/myapp/deploy`





