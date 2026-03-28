# Kubernetes Replica Set

---
## Write rs Yaml File 
~~~sh
nano rs.yaml
~~~
~~~sh
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: test-rs
  namespace: test
spec:
  replicas: 3
  selector:
    matchLabels:
      app: test-app
  template:
    metadata:
      labels:
        app: test-app
    spec:
      containers:
      - name: test-container
        image: nginx
        ports:
        - containerPort: 80

~~~
## Apply rs yaml file
~~~sh
kubectl apply -f rs.yaml
~~~
## Check rs
~~~sh
kubectl get rs -n test
~~~
## check pods namespace
~~~sh
kubectl get pods -n test
~~~
## delete rs
~~~sh
kubectl delete pod test -rs
~~~
