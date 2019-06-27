Vagrant.configure("2") do |config|
  config.vm.provider "virtualbox" do |v|
    v.memory = 2048
    # The AWS api forces signed requests to be no older than 5 minutes. If you leave a vagrant VM running while your
    # host OS sleeps, you can experience a drastic time skew on the guest OS.
    #
    # This forces the system time to sync every 10 seconds as opposed to the default 20 minutes.  If you still
    # experience AWS 400 errors, the solution is to run `vagrant reload`.
    v.customize [ "guestproperty", "set", :id, "/VirtualBox/GuestAdd/VBoxService/--timesync-set-threshold", 10000 ]

    # Some host OSs have experienced read-only shared mounts.  This seems to mitigate the problem
    v.customize [ "setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/vagrant", "1" ]
    v.customize [ "setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/home/vagrant/deep-dive", "1" ]

    # Remote files seem to download slowly without these settings
    v.customize [ "modifyvm", :id, "--natdnshostresolver1", "on" ]
    v.customize [ "modifyvm", :id, "--natdnsproxy1", "on" ]
  end
  config.vm.hostname = "playground"
  config.vm.box = "ubuntu/xenial64"

  config.vm.boot_timeout = 120

  config.vm.synced_folder "./", "/home/vagrant/deep-dive"

  # OSX needs this for concurrent open files
  config.vm.provision :shell, :inline => "ulimit -n 4048"

  # This is needed for windows 7 (not sure about later versions)
  config.vm.provision :shell, :inline => <<-SHELL
    echo 'Acquire::ForceIPv4 "true";' | tee /etc/apt/apt.conf.d/99force-ipv4
  SHELL
end
