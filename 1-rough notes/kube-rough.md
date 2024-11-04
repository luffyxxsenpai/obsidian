# kubernets rough notes

day1
kubectl get pod/deploy/rs/ns/svc
kubectl apply -f some.yaml
kubectl delete -f some.yaml
kubectl delete deploy nginx

kubectl  config set-context --current --namespace=myspace
kubectl api-respurces | grep pod/ns/rs/svc/deploy

kubectl port-forward mypod1  mymachineport:LiContainer: port
kubectl exec -it mypod -c mycontainer --bash

kubectl rollout history deployment my-static-site
kubectl rollout undo  deployment my-static-site
kubectl rollout undo  4 deployment my-static-site

minikube service myservice

 labels and selectors 
containerport = port on which the container is running 

deployment -> rollback and rollout


### day2
service 
 - abstract the pod ip from users
 - as long as svc exist ip wont change
 - also does the load balencing
 - service discovery 
 - zero downtime deployment

```bash
  ports:
    - port: 80
      targetPort: 80
```
port = the port service will recieve request on
targetport = the port on which container is running

TYPE OF SERVICE
1. cluster ip service = internal routing only , if not defined this will be applied
2. nodeport =  
3. loadbalencer = 


#### day3

k rollout restart deployment mygoenv -n myspace
configmaps
secrets

volumes 
emptydir  = volume inside pod
hostpath = volume inside node

  accessMode:
    - ReadWriteMany
    - ReadWriteOnce
    - ReadOnlyOnce
    - ReadOnlyMany
    - ReadWriteOncePod




