nodes = [
  # Les machines du cluster
  { :hostname => 'master-1', :ip => '192.168.76.3', :ram => 1024, :cpus => 1 },
  { :hostname => 'worker-1', :ip => '192.168.76.4', :ram => 1024, :cpus => 1 }
]

Vagrant.configure("2") do |config|
  
  config.ssh.insert_key = false
  # Mise en place d'une connexion ssh pour la communication entre les machines
  config.ssh.forward_agent = true
  # Provision des nœuds
  nodes.each do |node|
    config.vm.define node[:hostname] do |nodeconfig|
      nodeconfig.vm.box = "bento/ubuntu-20.04";
      nodeconfig.vm.hostname = node[:hostname] + ".box"
      nodeconfig.vm.network :private_network, ip: node[:ip]
      memory = node[:ram] ? node[:ram] : 1024;
      cpus = node[:cpus] ? node[:cpus] : 1;
      nodeconfig.vm.provider :virtualbox do |vb|
        vb.customize [
          "modifyvm", :id,
          "--memory", memory.to_s,
          "--cpus", cpus.to_s
        ]
      end
    end
  end
end
