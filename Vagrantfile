Vagrant.configure("2") do |config|
	config.vm.boot_timeout = 150

	config.vm.box = "puppetlabs/debian-7.8-64-puppet"
	# default password for user 'root': puppet

	# config.vm.network "public_network"
	config.vm.network "forwarded_port", guest: 80, host: 8080
	config.vm.network "private_network", ip: "192.168.56.4"
	# config.vm.synced_folder "www/", "/var/www", create: true, group: "www-data", owner: "www-data"

	config.vm.hostname = "vagrant"

	config.vm.provision "shell", inline: <<-SHELL
sudo apt-get update
sudo apt-get -y install puppet
sudo puppet apply --templatedir=/vagrant/puppet/templates --modulepath=/vagrant/puppet/modules/ /vagrant/puppet/manifests/nodes/vagrant.node
	SHELL

	config.vm.provider "virtualbox" do |vb|
		vb.customize ["modifyvm", :id, "--cpuexecutioncap", "70"]
		vb.customize ["modifyvm", :id, "--memory", 1024]
	end

end

