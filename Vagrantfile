# -*- mode: ruby -*-
# vi: set ft=ruby :



SWIFT_VERSION = "swift-3.0.2-RELEASE"
SWIFT_URL = "https://swift.org/builds/swift-3.0.2-release/ubuntu1404/swift-3.0.2-RELEASE/swift-3.0.2-RELEASE-ubuntu14.04.tar.gz"

Vagrant.configure(2) do |config|

    config.vm.box = "ubuntu/trusty64"

    config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
        vb.gui = false
        # Customize the amount of memory on the VM:
        vb.memory = "1024"
    end

    config.vm.provision "fix-no-tty", type: "shell" do |s|
        s.privileged = false
        s.inline = "sudo sed -i '/tty/!s/mesg n/tty -s \\&\\& mesg n/' /root/.profile"
    end

    # Aprovisionamiento inline
    config.vm.provision "shell", inline: <<-SHELL
        sudo apt-get -y install -f clang libicu-dev
        wget -q #{SWIFT_URL}
        tar xzf #{SWIFT_VERSION}-ubuntu14.04.tar.gz
        sudo chown -R vagrant #{SWIFT_VERSION}-ubuntu14.04 
        sudo mv #{SWIFT_VERSION}-ubuntu14.04 /usr/local 
        echo "export PATH=/usr/local/#{SWIFT_VERSION}-ubuntu14.04/usr/bin:\"${PATH}\"" >> /home/vagrant/.bashrc
    SHELL
end
