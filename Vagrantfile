machines = {
  "Server_Principal" => {"memory" => "512", "cpu" => "1", "ip" => "200", "image" => "efalia/linux-base-server"},
  "VM_1" => {"memory" => "512", "cpu" => "1", "ip" => "201", "image" => "efalia/linux-base-server"},
  "VM_2" => {"memory" => "512", "cpu" => "1", "ip" => "202", "image" => "efalia/linux-base-server"},
  "VM_3" => {"memory" => "512", "cpu" => "1", "ip" => "202", "image" => "efalia/linux-base-server"},
}

Vagrant.configure("2") do |config|

  machines.each do |name, conf|
    config.vm.define "#{name}" do |machine|
      machine.vm.box = "#{conf["image"]}"
      machine.vm.hostname = "#{name}"
      machine.vm.network "private_network", ip: "192.168.0.#{conf["ip"]}"
      machine.vm.provider "virtualbox" do |vb|
        vb.name = "#{name}"
        vb.memory = conf["memory"]
        vb.cpus = conf["cpu"]
        
      end
      machine.vm.provision "shell", path: "docker.sh"
      
      if "#{name}" == "server_Principal"
        machine.vm.provision "shell", path: "Server_Principal.sh"
      else
        machine.vm.provision "shell", path: "VM.sh"
      end

    end
  end
end
