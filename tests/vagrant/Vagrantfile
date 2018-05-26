require 'yaml'

machineConfig = YAML.load_file('config.yml')

Vagrant.configure("2") do |config|

  machineConfig.each do |m|
    settings = m[1]
    name = settings['name']
    
    config.vm.define name do |cfg|

      cfg.vm.box = settings['box']
      cfg.vm.network "public_network", bridge: "enp2s0", ip: settings['ip']

      cfg.vm.provider "virtualbox" do |vb|
            vb.gui = settings['gui']
            vb.memory = settings['memory']
            vb.cpus = settings['cpus']
      end
       
      cfg.vm.provision "shell", 
        inline: "sudo apt-get update && apt-get install -y python"

      cfg.vm.provision :ansible do |ansible|
        ansible.playbook = "deploy-keys.yml"
      end    

    end
    
  end

end
