Vagrant.configure("2") do |config|
  config.vm.box = "debian/bullseye64"

  # Máquina maestro
  config.vm.define "NGINX" do |tierra|
    tierra.vm.hostname = "NGINX.sistema.test"
    tierra.vm.network "public_network", ip: "192.168.122.170"
    tierra.vm.provider "virtualbox" do |vb|
      vb.name = "NGINX"
    end
    tierra.vm.provision "shell", inline: <<-SHELL
      sudo apt-get update -y
      sudo apt-get install nginx -y
      sudo apt-get install git -y
      sudo systemctl status nginx
      sudo mkdir -p /var/www/amz/html
      cd /var/www/amz/html
      git clone https://github.com/cloudacademy/static-website-example
      sudo chown -R www-data:www-data /var/www/amz/html
      sudo chmod -R 755 /var/www/amz
      sudo cp /vagrant/config/amz /etc/nginx/sites-available/amz
      sudo ln -s /etc/nginx/sites-available/amz /etc/nginx/sites-enabled/
      sudo systemctl restart nginx
      sudo systemctl status nginx
    SHELL
  end
end