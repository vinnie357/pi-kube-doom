# make a test deployment
 https://ubuntu.com/tutorials/install-a-local-kubernetes-with-microk8s#1-overview

  microk8s kubectl create deployment microbot --image=dontrebootme/microbot:v1
  microk8s kubectl scale deployment microbot --replicas=2
  microk8s kubectl expose deployment microbot --type=ClusterIP --port=80 --name=microbot-service

## or

```bash
k apply -f k8s/test/deployment-microbot.yaml
k apply -f k8s/test/service-microbot.yaml
k apply -f k8s/test/ingress-microbot.yaml
```
