IMAGE_NAME = "bento/ubuntu-18.04"

MASTER_IP = "192.168.100.10"

NodeCount = 1 # number of nodes you want

Vagrant.configure("2") do |config|
    config.ssh.insert_key = false
    config.vm.boot_timeout = 600

    config.vm.provider "virtualbox" do |v|
        # define cpu and memory for vms. Enable multiple processors and DNS resolution via the VM host and not direct (for peformance)
        v.customize ["modifyvm", :id, "--memory", "8192", "--cpus", "4", "--ioapic", "on", "--natdnshostresolver1", "on", "--natdnsproxy1", "on"]
    end
      
    config.vm.define "master" do |master|
        master.vm.box = IMAGE_NAME
        master.vm.network "private_network", ip: MASTER_IP
        master.vm.hostname = "master"
        master.vm.provision "ansible" do |ansible|
            ansible.playbook = "ansible/master.yml"
            ansible.extra_vars = {
                node_ip: MASTER_IP,
            }
        end
    end

    (1..NodeCount).each do |i|
        config.vm.define "node-#{i}" do |node|
            node.vm.box = IMAGE_NAME
            node.vm.network "private_network", ip: "192.168.100.#{i + 10}"
            node.vm.hostname = "node-#{i}"
            node.vm.provision "ansible" do |ansible|
                ansible.playbook = "ansible/node.yml"
                ansible.extra_vars = {
                    node_ip: "192.168.100.#{i + 10}",
                }
            end
        end
        
    config.vm.define "master" do |master|
    master.vm.provision "ansible" do |ansible|
        ansible.playbook = "ansible/deploy.yml"
        ansible.extra_vars = {
            node_ip: MASTER_IP,
        }
                end
            end
        end
    end