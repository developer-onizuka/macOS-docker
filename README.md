# 1. Install the VirtualBox

# 2. Install the Vagrant

# 3. Edit the Vagrantfile
```
Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-22.04"
  config.ssh.forward_x11 = true
  config.vm.hostname = "ubuntu2204"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = 16384
    vb.cpus = 6
  end

  config.vm.provision "shell", inline: <<-SHELL
    apt update
    #apt install -y ubuntu-desktop 
    apt install -y docker.io
    apt install -y git 
    apt install -y software-properties-common
    apt-add-repository --yes --update ppa:ansible/ansible
    apt install -y ansible
    apt install -y curl
    curl -LO https://github.com/kubernetes/minikube/releases/latest/download/minikube-linux-arm64
    sudo install minikube-linux-arm64 /usr/local/bin/minikube && rm minikube-linux-arm64
    usermod -aG docker vagrant
    cat <<EOF >> /home/vagrant/.bashrc 
alias kubectl="minikube kubectl --"
source <(kubectl completion bash) 
export XAUTHORITY=/home/vagrant/.Xauthority
EOF
    apt install -y bash-completion 
    apt install -y xserver-xorg x11-xserver-utils x11-apps
    cat <<EOF >> /etc/ssh/sshd_config
X11Forwarding yes
X11DisplayOffset 10
X11UseLocalhost no
EOF
    apt install chromium-browser
    #apt install -y xauth xdg-utils snapd
    #sudo apt install -y firefox firefox-locale-ja
  SHELL
end
```

# 4. Run VM
```
# vagrant up
```

# 5. Connect the VM
```
# vagrant ssh
```

# 6. Run the jupyter notebook
```
sudo docker run -it --rm -p 8888:8888 --user root -e GRANT_SUDO=yes --name notebook jupyter/base-notebook
```

# 7. Try some notebook
Do some git clone with the terminal in the jupyter notebook which you run.

