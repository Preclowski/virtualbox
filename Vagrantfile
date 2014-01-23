Vagrant.configure("2") do |config|

    # Box configuration. (Ubuntu 13.10 x64)
    config.vm.box       = "saucy64"
    config.vm.box_url   = "http://cloud-images.ubuntu.com/vagrant/saucy/current/saucy-server-cloudimg-amd64-vagrant-disk1.box"

    # Mount environment folder with correct permissions.
    config.vm.synced_folder ".", "/vagrant", owner: "vagrant", group: "vagrant"

    # Primary web server.
    config.vm.define "web" do |web|

        # Network configuration.
        web.vm.network :forwarded_port, host: 8080, guest: 80
        web.vm.network :forwarded_port, host: 3360, guest: 3306

        # Ansible provisioning.
        web.vm.provision "shell", path: "setup.sh"

    end

    config.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
        vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
    end
end
