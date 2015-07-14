$script = <<SCRIPT
yum install -y autoconf automake btrfs-progs gettext-devel git libtool
fallocate -l 10G ~/btrfs.img
mkdir /var/bocker
mkfs.btrfs ~/btrfs.img
mount -o loop ~/btrfs.img /var/bocker
git clone https://github.com/karelzak/util-linux.git
cd util-linux
git checkout tags/v2.25.2
./autogen.sh
./configure --without-ncurses --without-python
make
cd ..
SCRIPT

Vagrant.configure(2) do |config|
	config.vm.box = 'puppetlabs/centos-7.0-64-nocm'
	config.ssh.username = 'root'
	config.ssh.password = 'puppet'
	config.ssh.insert_key = 'true'
	config.vm.provision 'shell', inline: $script
end
