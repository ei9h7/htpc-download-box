$script = <<-SCRIPT
apt-get update
apt-get install git docker docker-compose -y
usermod -aG docker vagrant
systemctl enable docker && systemctl start docker
mkdir -p /media/data
mount -t ext4 -o defaults,auto,rw,nosuid,nodev,nofail UUID=a701ad27-a24e-4c53-85f7-eeca4ede86ad /media/data
chown -R vagrant:vagrant /media/data
git clone https://github.com/ei9h7/media-server.git /home/vagrant/media-server
chown -R vagrant:vagrant /home/vagrant/media-server
cd media-server
cp .env.example .env
docker-compose up -d
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "generic/ubuntu2104"
  config.vm.allow_fstab_modification= true
  config.vm.provision "shell", inline: $script
  config.vm.network "private_network", ip: "192.168.7.7"

end
