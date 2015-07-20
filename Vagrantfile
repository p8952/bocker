$script = <<SCRIPT
(
rpm -i https://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-5.noarch.rpm
yum install -y -q autoconf automake btrfs-progs docker gettext-devel git libtool python-pip

fallocate -l 10G ~/btrfs.img
mkdir /var/bocker
mkfs.btrfs ~/btrfs.img
mount -o loop ~/btrfs.img /var/bocker

pip install git+https://github.com/larsks/undocker
systemctl start docker.service
docker pull busybox
docker save busybox | undocker -o base-image
rm -rf /vagrant/base-image
mv base-image /vagrant || true

git clone https://github.com/karelzak/util-linux.git
cd util-linux
git checkout tags/v2.25.2
./autogen.sh
./configure --without-ncurses --without-python
make
mv unshare /usr/bin/unshare
cd ..
) 2>&1
SCRIPT

Vagrant.configure(2) do |config|
	config.vm.box = 'puppetlabs/centos-7.0-64-nocm'
	config.ssh.username = 'root'
	config.ssh.password = 'puppet'
	config.ssh.insert_key = 'true'
	config.vm.provision 'shell', inline: $script
end
