# install kubernetes

## option 1 SNAPs
  
  https://microk8s.io/docs/

  https://microk8s.io/docs/install-alternatives
  
  ```bash 
  #Raspberry Pi/ARM
  #Running MicroK8s on some ARM hardware may run into difficulties because cgroups (required!) are not enabled by default. This can be remedied on the Rasberry Pi by editing the #boot parameters: 
  #https://askubuntu.com/questions/1189480/raspberry-pi-4-ubuntu-19-10-cannot-enable-cgroup-memory-at-boostrap
  
  ## old
  #echo 'cgroup_enable=memory cgroup_memory=1' >> /boot/firmware/cmdline.txt
  #sudo sh -c "echo 'cgroup_enable=memory cgroup_memory=1' >> /boot/firmware/cmdline.txt"
  #reboot to take effect
  #sudo reboot
  ## check with
  #cat /proc/cmdline
  #if it doesn't work the first time make sure your arguments are all on one line and reboot again.  
  sudo snap install microk8s --classic
  sudo microk8s.status --wait-ready
  sudo microk8s.enable dns dashboard registry
  ```
  ### commands

  microk8s.kubectl command

  ## alias commands to k
  ```bash
  sudo apt-get install bash-completion -y
  echo 'source <(microk8s.kubectl completion bash)' >>~/.bashrc

  echo 'alias k=/snap/bin/microk8s.kubectl' >>~/.bash_aliases
  echo 'alias k=/snap/bin/microk8s.kubectl' >>~/.bashrc
  echo "alias kubectl='microk8s.kubectl'" >>~/.bashrc
  echo 'source ~/.bashrc' >> ~/.bash_profile
  #source ~/.bashrc
  ```
  ```bash
  sudo sh -c "echo 'cgroup_enable=memory cgroup_memory=1' >> /boot/firmware/cmdline.txt"
  sudo snap install microk8s --classic
  # add your user to microk8s
  sudo usermod -a -G microk8s $USER
  sudo chown -f -R $USER ~/.kube
  # log out and log back in or start a new shell
  source ~/.bashrc
  # check install status
  microk8s status --wait-ready
  # check what is avaliable
  # microk8s enable --help
  # install services
  microk8s enable dashboard dns registry storage helm3 ingress
  # disable
  # microk8s disable <service>
  microk8s kubectl get all --all-namespaces
  # alias k='microk8s kubectl'
  # alias kubectl='microk8s.kubectl'
  # with aliases
  k get all --all-namespaces
  ```