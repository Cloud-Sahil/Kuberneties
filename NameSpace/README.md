# Kubernetes NameSpace
---
## Namespaces provide a way to divide cluster resources between multiple users or teams.

## Default Namespaces
 - default: The default namespace for resources without a namespace.
 - kube-system: For Kubernetes system resources.
 - kube-public: For publicly accessible resources.

## Creating a Namespace
~~~sh
apiVersion: v1
kind: Namespace
metadata:
  name: my-namespace
~~~
