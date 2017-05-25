# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure("2") do |config|

    config.vm.box = "google/gce"
    config.ssh.forward_agent = true

    config.vm.provider :google do |google, override|
    google.google_project_id = "vagrant-168620"
    google.google_client_email = "vagrant@vagrant-168620.iam.gserviceaccount.com"
    google.google_json_key_location = "/Users/jruels/creds/vagrant-a46870ac43b5.json"
    google.image = "ubuntu-1604-xenial-v20170516"
    google.machine_type = "n1-standard-2"
    google.disk_size = "30"
    google.can_ip_forward = "true"

    override.ssh.username = "jruels"
    override.ssh.private_key_path = "/Users/jruels/.ssh/id_rsa"
    end
    config.vm.provision :ansible do |ansible|
        ansible.host_key_checking = false
        ansible.playbook = "devstack.yml"
        ansible.verbose = "v"
    end
    config.vm.provision :shell, :inline => "cd devstack; sudo -u vagrant env HOME=/home/vagrant ./stack.sh"
    config.vm.provision :shell, :inline => "ovs-vsctl add-port br-ex eth2"
    config.vm.provision :shell, :inline => "virsh net-destroy default"

end
