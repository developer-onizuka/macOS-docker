# 1. Install the VirtualBox

# 2. Install the Vagrant

# 3. Edit the Vagrantfile
```
Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-22.04"
  config.vm.hostname = "ubuntu2204"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = 16384
    vb.cpus = 4
  end
  config.vm.provision "shell", inline: <<-SHELL
    apt update
    apt install -y docker.io
    apt install -y curl
    apt install -y git 
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

