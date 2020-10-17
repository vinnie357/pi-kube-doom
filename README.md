# pi-kube-doom
excuse to play with kube-doom on a single node rpi4-k8s 
## Overview:
  
  excuse to setup kube doom on a single node k8s cluster running on raspberry pi, will attempt to cover assumptions about hardware and other setup with readmes and steps.

## Status

  well seems like ARM64 was left out of all of these parties, so going to see if I can't build some arm versions.
  ideally ending in docker images we can run on the pi.
  going to hack on that in my [fork](https://github.com/vinnie357/kubedoom) 
  
  [(I have no idea what I am doing dog)](https://i2.wp.com/gaxstudio.com/wp-content/uploads/2017/08/i-have-no-idea-what-im-doing-dog-feat-1-620x400.jpg?ssl=1)

## FAQ

  - Yes, there are other ways to do each part of this.( pxe boot, images, etc..)
    - I welcome Pull Requests showing the addtional ways to do each part
  - Yes, you can do this with a cluster. my hope was to lower the barriers to entry.

## hardware:

[canakit rpi4 4/8gig](https://www.canakit.com/raspberry-pi-4-starter-kit.html)

## software:

- [Ubuntu 20.04.1 LTS ARM](https://ubuntu.com/download/server/arm)
- [storax/kubedoom](https://github.com/storax/kubedoom)
- [NGINX](https://www.nginx.com/)
- [balana Etcher](https://www.balena.io/etcher/)
- [raspberrypi imager](https://www.raspberrypi.org/downloads/)
- [grafana](https://grafana.com/)

## setup overview:
 
 Break down for each is in their respective folders
  - [hardware](hardware/readme.md)
    - download ubuntu 20.04 and clone install to flash media in canakit.
    - base rpi4 setup
      - remote access
      - ssh keys
      - network config
  - [software](software/readme.md)
    - [k8s](software/k8s/readme.md)
      - setup single node k8s
        - persistent storage?
      - deploy services to cluster
        - grafana
        - kube doom
        - nginx ingress
      - expose services with nignx ingress
        - kube doom
        - grafana dashboard
    - [kubedoom](software/kubedoom/readme.md)
      - play kube doom! ( likely the most important part of all of this)
