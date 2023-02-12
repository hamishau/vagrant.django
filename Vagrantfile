Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/jammy64"
  config.vm.synced_folder ".", "/yourapp", :mount_options => ["dmode=777", "fmode=666"]
  config.vm.hostname = "yourapp.local"
  config.vm.network "forwarded_port", guest: 8080, host: 8080
  config.vm.network "private_network", ip: "192.168.56.10"
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt update
    sudo apt upgrade -y
    sudo apt install -y python3-pip
    sudo apt install -y build-essential libssl-dev libffi-dev python3-dev
    cd /yourapp
    sudo apt install -y postgresql postgresql-contrib
    sudo -u postgres createdb yourapp
    sudo -u postgres psql -c "ALTER USER postgres WITH PASSWORD 'admin';"
    pip3 install django
    pip3 install psycopg2-binary
    django-admin startproject yourapp .
  SHELL
end
