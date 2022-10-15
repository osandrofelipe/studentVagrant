# -*- mode: ruby -*-
# vi: set ft=ruby :

$script = <<-EOF
sudo yum -y update
sudo yum install -y epel-release
sudo yum install nginx -y
sudo systemctl start nginx
EOF

machines = {
  "ApacheServer" => {"memory" => "512", "cpu" => "1", "ip" => "222", "image" => "ubuntu/bionic64"},
 # "NginxServer" => {"memory" => "512", "cpu" => "1", "ip" => "223", "image" => "debian/jessie64"},
  "CentOS7" => {"memory" => "512", "cpu" => "1", "ip" => "224", "image" => "centos/7"}
}

Vagrant.configure("2") do |config|

  machines.each do |name, conf|
    config.vm.define "#{name}" do |machine|
      machine.vm.box = "#{conf["image"]}"
      machine.vm.hostname = "#{name}.SF.dev"
      machine.vm.network "public_network", ip: "192.168.0.#{conf["ip"]}"
      machine.vm.provider "virtualbox" do |vb|
        vb.name = "#{name}"
        vb.memory = conf["memory"]
        vb.cpus = conf["cpu"]
       
        if "#{name}" == "ApacheServer"
          machine.vm.provision "shell", inline: "sudo apt-get update && sudo apt-get install apache2 -y"
        end
        if "#{name}" == "CentOS7"
          machine.vm.provision "shell", inline: $script
        end
     end
    end
  end
end
