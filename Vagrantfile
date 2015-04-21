Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"
  
  config.vm.network :forwarded_port, guest: 8080, host: 8888
  
  config.vm.provision "chef_solo" do |chef|
    chef.add_recipe "java"
    chef.add_recipe "tomcat"
	
	chef.json = {
	  :java => {
	    :jdk_version => '8',
		:install_flavor => 'oracle',
		:oracle => {
		  :accept_oracle_download_terms => 'true'
		},
		:java_home => '/usr/lib/jvm/java-8-oracle-amd64',
		:set_etc_environment => 'true'
      },
	  :tomcat => {
	    :base_version => '7'
	  }
    }
  end
end