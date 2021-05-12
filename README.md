# Installing PMEM CSI Driver Operator on OpenShift

# Prereqs

* Nodefeature discovery operator installed and enabled. **Or** manually `oc label node <node-name> feature.node.kubernetes.io/memory-nv.dax=true`

# Installation

* Open a window and run

```bash
$ oc get events -n pmem-csi -w # be patient
```

* Open a second window and run

```bash
$ oc apply -k base
namespace/pmem-csi created
rolebinding.rbac.authorization.k8s.io/system:openshift:scc:privileged created
operatorgroup.operators.coreos.com/operatorgroup created
catalogsource.operators.coreos.com/operatorhubio-catalog created
subscription.operators.coreos.com/pmem-csi created
pmemcsideployment.pmem-csi.intel.com/pmem-csi.intel.com created
```

# Start Over

```bash
$ kustomize build base | oc delete -f -
$ oc apply -k base
```

# Debugging

```bash
$ oc get catalogsources -n openshift-marketplace

$ oc project pmem-csi

$ oc get ip
$ oc get csv
$ oc status
$ oc get events
$ oc get pods
$ oc logs deployment/pmem-csi-operator
$ oc logs sts/pmem-csi-intel-com-controller
$ oc logs ds/pmem-csi-intel-com-node --all-containers
```