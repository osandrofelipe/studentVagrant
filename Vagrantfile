# -*- mode: ruby -*-
# vi: set ft=ruby :

$script = <<-EOF
sudo yum -y update
sudo yum install -y epel-release
sudo yum install nginx -y
sudo systemctl start nginx
EOF

#$script_apache = <<-EOF
#sudo yum update
#sudo yum install apache2 -y
#EOF

#Vagrant.configure("2") do |config|
  
#  config.vm.define "nginx" do |nginx|
#    nginx.vm.box = "ubuntu/bionic64"
#    nginx.vm.hostname = "nginxDev"
#    nginx.vm.network "public_network"
#    nginx.vm.provision "shell", inline: $script_nginx
#  end

#  config.vm.define "apache" do |apache|
#    apache.vm.box = "centos/7"
#    apache.vm.network "public_network"
#    apache.vm.provision "shell", inline: $script_apache
#  end
 
  # config.vm.synced_folder "../data", "/vagrant_data"
#end


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
  #      vb.customize ["modifyvm", :id, "--groups", "/Docker-Lab"]
      
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
