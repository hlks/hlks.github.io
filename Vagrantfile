
$script = <<SCRIPT

yum install -y epel-release
yum update -y

yum install -y gcc-c++ patch readline readline-devel zlib zlib-devel libyaml-devel libffi-devel openssl-devel make bzip2 autoconf automake libtool bison iconv-devel

yum install -y nodejs npm

gpg2 --keyserver hkp://keys.gnupg.net --recv-keys D39DC0E3
curl -L get.rvm.io | bash -s stable

source /etc/profile.d/rvm.sh
rvm install 2.1.2
rvm use 2.1.2 --default
gem install jekyll
gem install github-pages

cd /vagrant && bundle install

cat <<EOF > /home/vagrant/.bashrc
# .bashrc

# Source global definitions
if [ -f /etc/bashrc ]; then
    . /etc/bashrc
fi

source /etc/profile.d/rvm.sh
cd /vagrant
EOF

cat <<EOF > /etc/motd
  ___________________________________
/ If at first the idea is not absurd, \
\ then there will be no hope for it   /
  -----------------------------------
         \   ^__^ 
          \  (oo)\_______
             (__)\       )\/\
                 ||----w |
                 ||     ||

Start jekyll:
jekyll serve --detach

...And then after changes:
jekyll build

http://1.2.4.4:4000

EOF

SCRIPT
 

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    config.vm.box = "centos-6.5"
    config.vm.box_url = "http://opscode-vm-bento.s3.amazonaws.com/vagrant/virtualbox/opscode_centos-6.5_chef-provisionerless.box"

    config.vm.network :private_network, :ip => "1.2.4.4"

    config.vm.provision :shell, :inline => $script

end
