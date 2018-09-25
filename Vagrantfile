VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    config.vm.box = "centos/7"
    config.vm.hostname = "vagrantbox"

    config.vm.network :forwarded_port, host: 80, guest: 80, auto_correct: true # website
    config.vm.network :forwarded_port, guest: 443, host: 443, auto_correct: true # ssl
    config.vm.network :forwarded_port, guest: 8080, host: 8080, auto_correct: true # Jenkins
    config.vm.network :private_network, ip: "10.0.0.10"

    config.vm.provision "ansible" do |ansible|
        ansible.playbook = "jenkins.yml"
        ansible.become = true
        #ansible.tags = "debug"
        #ansible.verbose = "vvvv"

        ansible.host_vars = {
              "default" => {"domain_name" => "jenkins.mydomain.com"}
            }
    end

    config.vm.provision :shell, inline: "echo Good job, now enjoy your new vbox: http://10.0.0.10"

end
