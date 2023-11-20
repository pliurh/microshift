Configure Log Verbosity for OVN-Kubernetes

The default log verbosity level in Microshift is set to `4` for OVN-Kubernetes
and `info` for OVN. You have the option to configure the log verbosity for
debugging and troubleshooting purposes. To do so, you can create a ConfigMap
named `env-overrides` with specific keys in the namespace
`openshift-ovn-kubernetes`, then restart the corresponding OVN-Kubernetes pods. 

Here's an example:

```yaml
kind: ConfigMap
apiVersion: v1
metadata:
  name: env-overrides
  namespace: openshift-ovn-kubernetes
  annotations:
data:
  # to set the log levels for the ovnkube-node pod
  # replace this with the node's name (from oc get nodes)
  ip-10-0-135-96.us-east-2.compute.internal: |
    OVN_LOG_LEVEL=dbg
  # to adjust the log levels for the ovnkube-master pod, use _master
  _master: |
    OVN_KUBE_LOG_LEVEL=5
    OVN_LOG_LEVEL=dbg
```