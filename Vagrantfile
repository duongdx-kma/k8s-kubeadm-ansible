NUM_MASTER_NODE = 1 # add standby master - recommend 3, 5, 7 master_node
# NUM_MASTER_NODE = 2 # add standby master - recommend 3, 5, 7 master_node
NUM_WORKER_NODE = 2

IP_NW = "192.168.56."
MASTER_IP_START = 1
NODE_IP_START = 5

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.vm.box_check_update = false

  # provision master node
  (1..NUM_MASTER_NODE).each do |i|
	config.vm.define "master0#{i}" do |node|
		node.vm.provider "virtualbox" do |vb|
			vb.name = "master0#{i}"
			vb.memory = 2048
			vb.cpus = 2
		end
		node.vm.hostname = "master0#{i}"
		node.vm.network :private_network, ip: IP_NW + "#{MASTER_IP_START + i}"
		node.vm.network "forwarded_port", guest: 22, host: "#{2710 + i}"

		#node.vm.provision "setup-container-runtime", type: "shell", :path => "ubuntu/install-docker.sh"
		node.vm.provision "setup-dns", type: "shell", :path => "ubuntu/update-dns.sh"
	end
  end


  # Provision Worker Nodes
  (1..NUM_WORKER_NODE).each do |i|
   config.vm.define "node0#{i}" do |node|
        node.vm.provider "virtualbox" do |vb|
            vb.name = "node0#{i}"
            vb.memory = 2048
            vb.cpus = 2
        end
        node.vm.hostname = "node0#{i}"
        node.vm.network :private_network, ip: IP_NW + "#{NODE_IP_START + i}"
        node.vm.network "forwarded_port", guest: 22, host: "#{2720 + i}"

        # node.vm.provision "setup-container-runtime", type: "shell", :path => "ubuntu/install-docker.sh"
        node.vm.provision "setup-dns", type: "shell", :path => "ubuntu/update-dns.sh"
    end
  end

  config.vm.provision "setup-deployment-user", type: "shell" do |s|
      ssh_pub_key = File.readlines("./ansible/client.pem.pub").first.strip
      s.inline = <<-SHELL
          # create deploy user
          useradd -s /bin/bash -d /home/deploy/ -m -G sudo deploy
          echo 'deploy ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers
          mkdir -p /home/deploy/.ssh && chown -R deploy /home/deploy/.ssh
          echo #{ssh_pub_key} >> /home/deploy/.ssh/authorized_keys
      SHELL
  end
end
