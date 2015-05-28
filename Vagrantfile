Vagrant.configure("2") do |config|
  config.vm.box = 'ubuntu/trusty64'
  
  config.vm.network :forwarded_port, guest: 8080, host: 8888
  
  config.vm.provision 'chef_solo' do |chef|
  
    # This box already has a suitable version of Chef, but I'm only disabling
	# installation because vagrant provisioning fails otherwise when in the
	# corporate environment
    chef.install = false
	
    chef.http_proxy = 'http://netservices.users.internal:3128'
    chef.https_proxy = 'http://netservices.users.internal:3128'
  
    #Not sure this is the way to do it
    #chef.recipe_url 'https://supermarket.chef.io/cookbooks'

    chef.add_recipe 'chef-solo-proxy'	
    chef.add_recipe 'java'
    chef.add_recipe 'tomcat'
	
	chef.json = {
      :chef_solo_proxy => {
        :https_proxy => 'http://netservices.users.internal:3128',
        :http_proxy => 'http://netservices.users.internal:3128'
      },
	  
	  :java => {
	    :jdk_version => '7',
		:install_flavor => 'oracle',
		:oracle => {
		  :accept_oracle_download_terms => true
		},
		:java_home => '/usr/lib/jvm/java-7-oracle-amd64',
		:jdk => {
		  :'7' => {
		   :x86_64 => {
		     :url => 'file://c:/Tools/jdk-7u79-linux-x64.tar.gz'
		   },
		  },
		},
      },
	  
	  :tomcat => {
	    :base_version => '7'
	  }
    }
  end
end