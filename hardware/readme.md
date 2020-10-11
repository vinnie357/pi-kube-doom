# setup
## unbox and setup your canakit!
  - link?
  - [example1](https://youtu.be/7rcNjgVgc-I?t=51)
    - 51 sec to 7:14
## setup flash media!
  - windows
    - download [raspberrypi imager](https://www.raspberrypi.org/downloads/)
    - or download [etcher](https://www.balena.io/etcher/)
    - download ubuntu server for arm [link](https://ubuntu.com/download/server/arm)
    - insert media into your computer with provided usb adapter
    - format media (the tools can do this for you)
    - burn image to flash media
## inital pi setup
  - connect the ethernet port on your raspberry pi for updates.
  - insert the flash media with the successful image
  - connect a monitor and keyboard
    - I use some cheap logitech wireless combos [logitech k235](https://www.amazon.com/Logitech-MK235-Wireless-Keyboard-Mouse/dp/B01AROOL12)
  - turn on your pi!
## configure pi
  - login and change the default password
    - ubuntu/ubuntu
    - collect the ipv4 address you see after logging in
  - create yourself a user and disable the ubuntu account
    ```bash
    # optional change default shell to bash
    # check it
    #sudo useradd -D | grep -i shell
    # change it
    # for all
    #sudo useradd -D -s /usr/bin/bash
    # for you
    #sudo usermod --shell /usr/bin/bash $myusername
    # check it
    #sudo useradd -D | grep -i shell
    myusername="notroot"
    sudo useradd $myusername
    sudo passwd $myusername
    sudo adduser $myusername sudo
    sudo adduser $myusername adm
    sudo chown -R $myusername:$myusername /home/$myusername
    ```
  - import your ssh public key from github or manually
    login as your user, or use su to run the commands as your user
    ```bash
    su - myusername
    ```
    ```bash
    gitusername="vinnie357"
    
    mkdir -p ~/.ssh/
    sudo chmod 700 ~/.ssh
    curl https://github.com/$gitusername.keys | tee -a  >> ~/.ssh/authorized_keys
    chmod 600 ~/.ssh/authorized_keys
    ```
    - remotely
    ```bash
    myuser="notroot"
    gitusername="vinnie357"
    server="targetipv4address"
    cat ~/.ssh/mykey.pub | ssh $user@$server 'mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys'
    mykeys=$(curl -s https://github.com/$gitusername.keys)
    echo "$mykeys" | ssh $user@$server 'mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys'
    ```
  - set hostname
    ```bash
    myhostname="k8sDoom"
    sudo hostnamectl set-hostname $myhostname
    ```
  - enable ssh
    depending on your install, you may need to enable ssh
    ```bash
    sudo apt install ssh
    sudo systemctl enable --now ssh
    sudo systemctl status ssh
    ```
    in either case you may want to rotate the default host keys
    ```bash
      sudo /bin/rm -v /etc/ssh/ssh_host_*
      sudo dpkg-reconfigure openssh-server
      sudo systemctl restart ssh
    ```
  - update os
    ```bash
    sudo apt-get -y update && sudo apt-get -y upgrade
    # reboot
    #sudo reboot
    ```