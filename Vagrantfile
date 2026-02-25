# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "digital_ocean"
  config.vm.define "Cosmotonic" do |kosmotonic|
    kosmotonic.vm.provider :digital_ocean do |provider|
      provider.token = ENV["DIGITAL_OCEAN_KEY"]
      provider.ssh_key_name = ENV["SSH_KEY_NAME"]

      provider.image = "ubuntu-22-04-x64"
      provider.region = "fra1"
      provider.size = "s-1vcpu-1gb"
    end
    config.ssh.private_key_path = '~/.ssh/id_ed25519'
    config.vm.synced_folder ".", "/vagrant", type: "rsync"

    config.vm.provision "shell", env: {"GIT_TOKEN" => ENV['GIT_TOKEN'], "DO_TOKEN" => ENV['DIGITAL_OCEAN_KEY']}, inline: <<-SHELL
      set -e
      
      while fuser /var/lib/apt/lists/lock >/dev/null 2>&1; do sleep 1; done   
      apt update
      apt install -y docker.io git curl
      
      cd /root
      
      if [ -d "cosmotonic" ]; then
        echo "Repo exists, pulling latest..."
        cd cosmotonic
        git pull
      else
        echo "Cloning repo..."
        git clone https://$GIT_TOKEN@github.com/Cosmotonic/cosmotonic.git
        cd cosmotonic
      fi
      
      docker build -t mysite .
      docker stop $(docker ps -q) || true
      docker run -d -p 80:80 mysite
    SHELL
  end
end