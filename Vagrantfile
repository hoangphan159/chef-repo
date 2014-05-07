Vagrant.configure("2") do |config|
	config.vm.box = "opscode-ubuntu-12.04"
	config.vm.box_url = "https://opscode-vm-bento.s3.amazonaws.com/vagrant/opscode_ubuntu-12.04_provisionerless.box"
	config.omnibus.chef_version = :latest

	config.vm.network "forwarded_port", guest: 9200, host: 19200
	config.vm.provision :chef_client do |chef|
		chef.json = {
			"java" => {
      				"install_flavor" => "oracle",
      				"jdk_version" => "7",
      				"accept_license_agreement" => true,
      				"oracle" => {
        				"accept_oracle_download_terms" => true
      				}
    			}
		}
		
		chef.add_recipe "apt"
		chef.add_recipe "java"	

		chef.provisioning_path = "/etc/chef"
		chef.chef_server_url = "https://api.opscode.com/organizations/hoangds"
		chef.validation_key_path = "./.chef/hoangds-validator.pem"
		chef.validation_client_name = "hoangds-validator"
		chef.node_name = "server"
	end
	
	config.vm.provider "virtualbox" do |v| 
  		v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
	end
end
