Vagrant.require_version ">= 2.2.2"

Vagrant.configure(2) do |config|

  # Using 'generic' for 'libvirt' provider support
  config.vm.box = "generic/ubuntu1804"
  #config.vm.box = "ubuntu/bionic64"

  config.vm.network "private_network", ip: "172.30.1.5"
  config.ssh.insert_key = false

  config.vm.provider "libvirt" do |lv|
  end

  # ==> default: Running provisioner: ansible_local...
  # `playbook` does not exist on the guest: /vagrant/nas.yml
  config.vm.synced_folder "./", "/vagrant/"

  config.vm.provision "ansible_local" do |ansible|
    ansible.compatibility_mode = "2.0"
    ansible.galaxy_role_file = "requirements.yml"
    ansible.playbook = "nas.yml"
    ansible.become = true
    ansible.raw_arguments = [
      "--extra-vars @tests/test.yml"
    ]
  end
end
