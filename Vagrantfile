Vagrant.configure(2) do |config|
  config.vm.box = "bento/centos-7.1"

  N = 4
  
  VAGRANT_VM_PROVIDER = "virtualbox"
  ANSIBLE_RAW_SSH_ARGS = []
  
  # (1..N-1).each do |machine_id|
  #   ANSIBLE_RAW_SSH_ARGS << "-o IdentityFile=#{ENV["VAGRANT_DOTFILE_PATH"]}/machines/machine#{machine_id}/#{VAGRANT_VM_PROVIDER}/private_key"
  # end

  (1..N).each do |machine_id|
    config.vm.define "machine#{machine_id}" do |machine|
      machine.vm.hostname = "machine#{machine_id}"
      machine.vm.network "private_network", ip: "192.168.33.#{9+machine_id}"
      if machine_id == N
        machine.vm.network  "forwarded_port", guest: 80, host: 8037
        machine.vm.provision :ansible do |ansible|
          ansible.playbook = "playbook.yml"
          # ansible.verbose = "vvv"
          ansible.limit = 'all'
          ansible.inventory_path = "hosts"
          # ansible.raw_ssh_args = ANSIBLE_RAW_SSH_ARGS
        end
      end
    end
  end
end