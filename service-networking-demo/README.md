Service Networking
```
diff --color -u advertisements.yaml  advertisements2.yaml
```
```
kubectl get deployments -n ns1 -l service=advertisements --show-labels
```
```
kubectl get pods -n ns1 -l service=advertisements --show-labels
```
```
kubectl get svc advertisements -n ns1 -o custom-columns="Name:metadata.name,Selector:spec.selector"
```
