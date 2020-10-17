# kubedoom

https://github.com/storax/kubedoom

## run docker

```bash
# x86
 docker run -p5901:5900 \
  --net=host \
  -v ~/.kube:/root/.kube \
  --rm -it --name kubedoom \
  storaxdev/kubedoom:0.5.0
# arm
docker run -p5901:5900 \
--net=host \
-v ~/.kube:/root/.kube \
--rm -it --name kubedoom \
kubedoom-arm:latest
```
## run in cluster

### build for microk8s registry

***note this is if you are running it in the cluster***

https://microk8s.io/docs/registry-built-in

in this example I am building the image localy based on the dockerfile.arm [here](https://github.com/vinnie357/kubedoom)

```bash
sudo apt install -y make
make buildarm
# wait for
#Successfully built bbf42bc438ee
#Successfully tagged kubedoom-arm:latest
```

tag the new build for the microk8s repo

```bash
docker tag bbf42bc438ee localhost:32000/kubedoom-arm:latest
docker push localhost:32000/kubedoom-arm
# wait for
#registry: digest: sha256:4bb99b0185614a214c5c624e563bc28aea5b9a46a82297de65d22a3ecdba27ff size: 2419
```

### running

***note it may take a moment for the namespace to create, just rerun the apply if you see: ***
```bash
Error from server (NotFound): error when creating "manifest/arm/deployment.yaml": namespaces "kubedoom" not found
```

```bash
# arm/pi
kubectl apply -f manifest/arm
# delete
# kubectl delete -f manifest/arm

# x86
kubectl apply -f manifest/x86

```

check your deployments

```bash
kubectl -n kubedoom get pods
# will see
NAME                       READY   STATUS    RESTARTS   AGE
kubedoom-667db567b-9446m   1/1     Running   0          2m41s
# logs
kubectl -n kubedoom logs kubedoom-667db567b-9446m --follow
### will see
***** game ticker: *****
Demon: ingress/nginx-ingress-microk8s-controller-sbn9t, 2110379302
Demon: default/microbot-deployment-5d8dc94754-nslwb, 1337757931
Demon: default/microbot-deployment-5d8dc94754-86h8z, 1271519629
Demon: default/microbot-deployment-5d8dc94754-vbsgl, 1346641475
Demon: kube-system/hostpath-provisioner-976f6d665-9vz7n, 1618746668
Demon: kube-system/calico-kube-controllers-847c8c99d-v699n, 7356115
Demon: kube-system/kubernetes-dashboard-7ffd448895-klgkf, 1602356208
Demon: kube-system/metrics-server-7b7db5984b-wv8cg, 363272515
Demon: container-registry/registry-675f6c55b6-nrgpj, 27290644
Demon: kube-system/dashboard-metrics-scraper-6c4568dc68-8w2qb, 1574800343
Demon: kube-system/coredns-86f78bb79c-4qp4h, 1116459616
Demon: kube-system/calico-node-rnznb, 1082750302
Demon: kubedoom/kubedoom-667db567b-9446m, 1581133579
```

### expose your service

quick:

```bash
kubectl -n kubedoom port-forward service/kubedoom-service 5901:5901
```
ingress TCP:

https://kubernetes.github.io/ingress-nginx/user-guide/exposing-tcp-udp-services/


## connect with VNC

default creds idbehold from docker build

linux

```bash
# docker
vncviewer viewer localhost:5900
# cluster
vncviewer viewer ingressip:5900
```

chrome plugin

[VNC® Viewer for Google Chrome™](https://chrome.google.com/webstore/detail/vnc%C2%AE-viewer-for-google-ch/iabmpiboiopbgfabjmgeedhcmjenhbla/related?hl=en)
