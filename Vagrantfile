VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.box_url = 'https://vagrantcloud.com/ubuntu/boxes/trusty64/versions/14.04/providers/virtualbox.box'
  
  config.vm.network :forwarded_port, guest:4444, host:4444
  config.vm.network :private_network, ip: "192.168.33.10"
  config.vm.provision "shell", path: "script.sh"
  #config.vm.synced_folder "/Users/ryan.gorsuch/dev/cms-scte-blackouts", "/srv/home/cms-scte-blackouts"
  config.vm.synced_folder "/Users/ryan.gorsuch/dev/scte", "/srv/home/cms-scte-blackouts"


  if OS.mac? 
    config.vm.provider :virtualbox do |vb|
      vb.gui = true
      vb.customize "pre-boot", [
        "storageattach", :id,
        "--storagectl", "SATAController",
        "--port", "1",
        "--device", "0",
        "--type", "dvddrive",
        "--medium", "/Applications/VirtualBox.app/Contents/MacOS/VBoxGuestAdditions.iso",
        #"--medium", "emptydrive"
        ]
    end
  end

end

module OS
    def OS.windows?
        (/cygwin|mswin|mingw|bccwin|wince|emx/ =~ RUBY_PLATFORM) != nil
    end

    def OS.mac?
        (/darwin/ =~ RUBY_PLATFORM) != nil
    end

    def OS.unix?
        !OS.windows?
    end

    def OS.linux?
        OS.unix? and not OS.mac?
    end
end
