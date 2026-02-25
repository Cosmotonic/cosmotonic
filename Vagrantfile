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
      rm -rf cosmotonic
      git clone https://$GIT_TOKEN@github.com/Cosmotonic/cosmotonic.git
      
      cd /root/cosmotonic
      docker build -t mysite .
      docker run -d -p 80:80 mysite
      
      curl -X POST "https://api.digitalocean.com/v2/reserved_ips/159.89.215.163/actions" \
        -H "Authorization: Bearer ${DO_TOKEN}" \
        -H "Content-Type: application/json" \
        -d '{"type":"assign","droplet_id":'$(curl -s http://169.254.169.254/metadata/v1/id)'}'
    SHELL
  end
end