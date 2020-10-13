Vagrant.configure(2) do |config|
    config.vm.box = "generic/debian10"
    config.vm.hostname = "vagrant-xen"
    config.vm.define "Xen"
    #config.ssh.private_key_path = "~/.ssh/id_rsa"
    #config.ssh.forward_agent = true

    # Build Xen from source
    xen_src = true
    # Version of Xen repo to checkout (tag, branch, etc...)
    xen_src_version = "stable-4.14"
    xen_force_build = false

    enabled_vms = {
      'winxp': true,
      'win7': false,
      'ubuntu': false,
    }

    config.vm.synced_folder ".", "/vagrant", disabled: true

    config.vm.provider :libvirt do |libvirt|
        libvirt.default_prefix = "Vagrant"
        libvirt.cpus = 2
        libvirt.cpu_mode = "host-passthrough"
        libvirt.cpu_fallback = "forbid"
        libvirt.memory = 3072
        libvirt.nic_model_type = "virtio"
        libvirt.driver = "kvm"
        libvirt.nested = true
    end

    config.vm.provider :hyperv do |hyperv|
        hyperv.vmname = "Vagrant"
        hyperv.cpus = 2
        hyperv.maxmemory = 3072
        hyperv.enable_virtualization_extensions = true
        hyperv.linked_clone = true
        hyperv.vlan_id = 3
    end

    config.vm.provision "ansible" do |ansible|
        ansible.compatibility_mode = "2.0"
        ansible.playbook = "./ansible/provision.yml"
        ansible.extra_vars = {
            'xen_src': xen_src,
            'xen_src_version': xen_src_version,
            'xen_force_build': xen_force_build,
            'enabled_vms': enabled_vms,
        }
    end
end
