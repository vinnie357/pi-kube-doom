# pi-kube-doom
excuse to play with kube-doom on a single node rpi4-k8s 
## Overview:
  
  excuse to setup kube doom on a single node k8s cluster running on raspberry pi, will attempt to cover assumptions about hardware and other setup with readmes and steps.
  
## hardware:

[canakit rpi4 4/8gig](https://www.canakit.com/raspberry-pi-4-starter-kit.html)

## software:

- [Ubuntu 20.04.1 LTS ARM](https://ubuntu.com/download/server/arm)
- [storax/kubedoom] (https://github.com/storax/kubedoom)
- [nginx] (https://www.nginx.com/)
- [balana Etcher](https://www.balena.io/etcher/)
- [grafana](https://grafana.com/)

## setup:

  - download ubuntu 20.04 and clone install to flash media in canakit.
  - base rpi4 setup
    - remote access
    - ssh keys
    - network config
  - setup single node k8s
    - persistent storage?
  - deploy services to cluster
    - grafana
    - kube doom
    - nginx ingress
  - expose services with nignx ingress
    - kube doom
    - grafana dashboard
  - play kube doom! ( likely the most important part of all of this)
