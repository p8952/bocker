$script = <<SCRIPT
(
rpm -i https://dl.fedoraproject.org/pub/epel/7/x86_64/Packages/e/epel-release-7-11.noarch.rpm
yum install -y -q autoconf automake btrfs-progs docker gettext-devel git libcgroup-tools libtool python-pip

fallocate -l 10G ~/btrfs.img
mkdir /var/bocker
mkfs.btrfs ~/btrfs.img
mount -o loop ~/btrfs.img /var/bocker

pip install git+https://github.com/larsks/undocker
systemctl start docker.service
docker pull centos
docker save centos | undocker -o base-image

git clone https://github.com/karelzak/util-linux.git
cd util-linux
git checkout tags/v2.25.2
./autogen.sh
./configure --without-ncurses --without-python
make
mv unshare /usr/bin/unshare
cd ..

ln -s /vagrant/bocker /usr/bin/bocker

echo 1 > /proc/sys/net/ipv4/ip_forward
iptables --flush
iptables -t nat -A POSTROUTING -o bridge0 -j MASQUERADE
iptables -t nat -A POSTROUTING -o enp0s3 -j MASQUERADE

ip link add bridge0 type bridge
ip addr add 10.0.0.1/24 dev bridge0
ip link set bridge0 up
) 2>&1
SCRIPT

Vagrant.configure(2) do |config|
	config.vm.box = 'puppetlabs/centos-7.0-64-nocm'
	config.ssh.username = 'root'
	config.ssh.password = 'puppet'
	config.ssh.insert_key = 'true'
	config.vm.provision 'shell', inline: $script
end
