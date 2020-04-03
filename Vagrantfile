# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do|config|
	config.ssh.insert_key = false
        config.hostmanager.enabled = false
        config.vm.provision :hostmanager
	config.vm.provider :virtualbox do|vb|
        	vb.customize ["modifyvm", :id, "--memory", "1048"]
	end

	#Puppet Server
        config.vm.define "puppetserver" do|puppetserver|
		puppetserver.vm.hostname = "puppetserver.lab.example.com"
		puppetserver.vm.box = "centos/7"
		puppetserver.vm.network "private_network", ip: "192.168.0.20"
		puppetserver.hostsupdater.aliases = ["puppetserver.lab.example.com", "puppetserver"]
		  config.vm.provider :virtualbox do|vb|
        	     vb.customize ["modifyvm", :id, "--memory", "2048"]
		  end
                puppetserver.vm.provision "shell", inline: <<-SHELL
		  rpm -Uvh https://yum.puppetlabs.com/puppet5/puppet5-release-el-7.noarch.rpm
                  yum install -y nano vim gcc puppet-agent ruby
                  sed -i "s/^PasswordAuthentication no/PasswordAuthentication yes/" /etc/ssh/sshd_config
                  systemctl restart sshd
	          /opt/puppetlabs/puppet/bin/gem install gpgme --no-rdoc --no-ri
  		  /opt/puppetlabs/puppet/bin/gem install hiera-eyaml-gpg --no-rdoc --no-ri
                  /opt/puppetlabs/puppet/bin/gem install r10k --no-rdoc --no-ri
                SHELL
	end


	#PuppetClient1 
	config.vm.define "puppetclient1" do|puppetclient1|
		puppetclient1.vm.hostname = "puppetclient1.lab.example.com"
		puppetclient1.vm.box = "centos/7"
		puppetclient1.vm.network "private_network", ip: "192.168.0.10"
		puppetclient1.hostsupdater.aliases = ["puppetclient1.lab.example.com", "puppetclient1"]
                puppetclient1.vm.provision "shell", inline: <<-SHELL
		  rpm -Uvh https://yum.puppetlabs.com/puppet5/puppet5-release-el-7.noarch.rpm
                  yum install -y nano vim gcc puppet-agent ruby
                  sed -i "s/^PasswordAuthentication no/PasswordAuthentication yes/" /etc/ssh/sshd_config
                  systemctl restart sshd
	          /opt/puppetlabs/puppet/bin/gem install gpgme --no-rdoc --no-ri
  		  /opt/puppetlabs/puppet/bin/gem install hiera-eyaml-gpg --no-rdoc --no-ri
                  /opt/puppetlabs/puppet/bin/gem install r10k --no-rdoc --no-ri
                SHELL
	end

	#PuppetClient2
	config.vm.define "puppetclient2" do|puppetclient2|
		puppetclient2.vm.hostname = "puppetclient2.lab.example.com"
		puppetclient2.vm.box = "centos/7"
		puppetclient2.vm.network "private_network", ip: "192.168.0.11"
		puppetclient2.hostsupdater.aliases = ["puppetclient2.lab.example.com", "puppetclient2"]
                puppetclient2.vm.provision "shell", inline: <<-SHELL
		  rpm -Uvh https://yum.puppetlabs.com/puppet5/puppet5-release-el-7.noarch.rpm
                  yum install -y nano vim gcc puppet-agent ruby
                  sed -i "s/^PasswordAuthentication no/PasswordAuthentication yes/" /etc/ssh/sshd_config
                  systemctl restart sshd
	          /opt/puppetlabs/puppet/bin/gem install gpgme --no-rdoc --no-ri
  		  /opt/puppetlabs/puppet/bin/gem install hiera-eyaml-gpg --no-rdoc --no-ri
                  /opt/puppetlabs/puppet/bin/gem install r10k --no-rdoc --no-ri
                SHELL
	end

	config.vm.box_check_update = false
#        config.vbguest.auto_update = true
end
