$mysql_install = <<~SCRIPT
  sudo ssh-keyscan github.com >> /home/vagrant/.ssh/known_hosts
  git clone git@github.com:vlmaslennikov/mysql-phpmyadmin.git 
  cd mysql-phpmyadmin
  git pull
  sudo ./mysql-phpmyadmin-install.sh $1 $2  
SCRIPT

$phpmyadmin_install = <<~SCRIPT
  sudo ssh-keyscan github.com >> /home/vagrant/.ssh/known_hosts
  git clone git@github.com:vlmaslennikov/mysql-phpmyadmin.git 
  cd mysql-phpmyadmin
  git pull
  sudo ./mysql-phpmyadmin-install.sh $1 $2 $3 $4 $5 
SCRIPT

Vagrant.configure(2) do |config|
  config.env.enable
  config.vm.box = ENV['VM_BOX']
  config.ssh.forward_agent = true

  # FIRST VM
  config.vm.define "mysql" do |mysql_config|
    mysql_config.vm.provider "virtualbox" do |vb|
      vb.name = "mysql"
    end
    mysql_config.vm.hostname = "mysql"    
    mysql_config.vm.provision "shell" do |s|
      s.inline = $mysql_install
      s.privileged = false
      s.args = "#{ENV['MYSQL_USER_PASSWORD']} #{ENV['MYSQL_ROOT_PASSWORD']}"  
    end
  end

  # SECOND VM
  config.vm.define "phpmyadmin" do |phpmyadmin_config|
    phpmyadmin_config.vm.provider "virtualbox" do |vb|
      vb.name = "phpmyadmin"
    end
    phpmyadmin_config.vm.hostname = "phpmyadmin"
    phpmyadmin_config.vm.provision "shell" do |s| 
      s.inline = $phpmyadmin_install 
      s.privileged = false
      s.args = "#{ENV['PHPMYADMIN_PASSWORD']} #{ENV['MYSQL_USER_NAME']} #{ENV['MYSQL_USER_PASSWORD']} #{ENV['MYSQL_DB_NAME']} #{ENV['MYSQL_HOST']}"
    end
  end
    
end
