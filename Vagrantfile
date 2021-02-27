IMAGE_NAME = "generic/ubuntu1804"
N = 2

Vagrant.configure("2") do |config|
    config.ssh.insert_key = false
      
    config.vm.define "k8s-master" do |master|
        master.vm.box = IMAGE_NAME
        master.vm.network "private_network", ip: "192.168.153.139"
        master.vm.hostname = "k8s-master"
        master.vm.provider "hyperv" do |h|
            h.memory = 2048
            h.cpus = 2
            h.enable_virtualization_extensions = false
            h.linked_clone = false
        end
        # master.vm.provision "ansible" do |ansible|
        #     ansible.playbook = "kubernetes-setup/master-playbook.yml"
        #     ansible.extra_vars = {
        #         node_ip: "192.168.153.139",
        #     }
        # end
    end

    (30..31).each do |i|
        config.vm.define "node-#{i}" do |node|
            node.vm.box = IMAGE_NAME
            node.vm.network "private_network", ip: "192.168.153.#{i + 10}"
            node.vm.hostname = "node-#{i}"
            node.vm.provider "hyperv" do |h|    
                h.memory = 1024
                h.cpus = 1
                h.enable_virtualization_extensions = false
                h.linked_clone = false
            end
            # node.vm.provision "ansible" do |ansible|
            #     ansible.playbook = "kubernetes-setup/node-playbook.yml"
            #     ansible.extra_vars = {
            #         node_ip: "192.168.153.#{i + 10}",
            #     }
            # end
        end
    end
end 