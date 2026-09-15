
# Имя бокса можно переопределить через переменную окружения:
#   VAGRANT_BOX=almalinux9-stand vagrant up --provider=libvirt
BOX_NAME = ENV['VAGRANT_BOX'] || 'ubuntu-jammy'

Vagrant.configure("2") do |config|
  # Ubuntu Jammy
  config.vm.define "ubuntu-jammy" do |srv|
    srv.vm.box = BOX_NAME

    srv.vm.provider "virtualbox" do |vb|
      vb.memory = 2048
      vb.cpus = 2
      vb.name = "ubuntu-vm"
      vb.customize ['modifyvm', :id, '--audio', 'none']
    end

    srv.vm.provider "libvirt" do |vb|
      vb.memory = 2048
      vb.cpus = 2
      vb.name = "ubuntu-vm"
      vb.customize ['modifyvm', :id, '--audio', 'none']
    end

    # Синхронизация папок
    srv.vm.synced_folder "./", "/vagrant"

    # Подключение диска
    srv.vm.disk :disk, size: "1GB", name: "disk1"
    srv.vm.disk :disk, size: "1GB", name: "disk2"

    # Проброс порта для HTTP (будет доступен по localhost:8080)
    srv.vm.network(:forwarded_port,
                    guest: 80,
                    host: 8080,
                    host_ip: "127.0.0.1")

    # Приватная сеть в той же подсети, что и virbr0 на хосте (192.168.122.0/24)
    srv.vm.network(:private_network,
                   ip: "192.168.56.11",
                   virtualbox__intnet: "dns",
                   libvirt__network_name: "dns",
                   libvirt__host_ip: "192.168.56.1",
                   libvirt__netmask: "255.255.255.0",
                   auto_config: true)

    # Provisioning - установка Apache
    srv.vm.provision "shell", inline: <<-SHELL

      # монтирование двух созданных дисков по 1Gb
      sudo parted -s /dev/sdb mklabel gpt mkpart primary 1MiB 100%
      sudo mkfs.ext4 -F /dev/sdb1
      sudo mkdir -p /mnt/disk1
      UUID=$(sudo blkid -s UUID -o value /dev/sdb1)
      sudo umount /mnt/disk1
      sudo mount UUID=$UUID /mnt/disk1
      sudo chmod -R 0777 /mnt/disk1
      sudo sed -i "/\/mnt\/disk1/d" /etc/fstab
      sudo echo "UUID=$UUID  \/mnt\/disk1  ext4  defaults,noatime,nodiratime  0  2" >> /etc/fstab

      sudo parted -s /dev/sdc mklabel gpt mkpart primary 1MiB 100%
      sudo mkfs.ext4 -F /dev/sdc1
      sudo mkdir -p /mnt/disk2
      UUID=$(sudo blkid -s UUID -o value /dev/sdc1)
      sudo umount /mnt/disk2
      sudo mount UUID=$UUID /mnt/disk2
      sudo chmod -R 0777 /mnt/disk2
      sudo sed -i "/\/mnt\/disk2/d" /etc/fstab
      sudo echo "UUID=$UUID  \/mnt\/disk2  ext4  defaults,noatime,nodiratime  0  2" >> /etc/fstab

      # Обновление пакетов
      sudo apt-get update
      
      # Установка Apache
      sudo apt-get install -y apache2
      
      # Отключаем стандартную папку /var/www/html
      sudo a2dissite 000-default.conf
      
      # Создаем конфигурацию для нашего сайта
      echo "<VirtualHost *:80>
          DocumentRoot /vagrant
          <Directory /vagrant>
              Options Indexes FollowSymLinks
              AllowOverride All
              Require all granted
          </Directory>
      </VirtualHost>" | sudo tee /etc/apache2/sites-available/vagrant.conf
      
      # Включаем наш сайт
      sudo a2ensite vagrant.conf
      
      # Включение mod_rewrite
      sudo a2enmod rewrite
      
      # Перезапуск Apache
      sudo systemctl restart apache2
    SHELL
  end
end
