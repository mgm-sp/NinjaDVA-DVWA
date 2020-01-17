# ninjaDVA dvwa


Vagrant.configure("2") do |config|

    #-------------------Your VM config----------------------------------
    config.vm.define "dvwa"

    # name and version of vm image
    config.vm.box = "bento/debian-10"

    # set hostname for vm
    config.vm.hostname = "dvwa"

    # disable standard synced folder
    config.vm.synced_folder ".", "/vagrant", disabled: true

    # install, build, and run docker
    config.vm.provision "docker" do |d|
      d.pull_images "vulnerables/web-dvwa"
      d.run "dvwa",
        image: "vulnerables/web-dvwa",
        args: "-it -p 80:80"
    end


    #----------------- ninjaDVA specific configuration -------------------------------
    # test whether the vm is started in ninjaDVA context
    # if yes copy challenges to dashboard vm
    if File.exists?("../ninjadva.rb")
      require "../ninjadva"
      NinjaDVA.new(
        config,
        {
          link_widget_links: [
            { :hostname => "dvwa", :name => "dvwa" },
          ]
        }
      )
    end

  end