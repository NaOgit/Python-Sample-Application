required_plugins = ["vagrant-omnibus"]
required_plugins = ["vagrant-berkshelf"]

required_plugins = ["vagrant-hostsupdater"]

required_plugins.each do |plugin|
  unless Vagrant.has_plugin?(plugin)
    puts "Installing vagrant plugin #{plugin}"
    Vagrant::Plugin::Manager.instance.install_plugin plugins
    puts "Installed vagrant plugin #{plugin}"
  end
end

Vagrant.configure("2") do |config|
  config.vm.define "app" do |app|
    app.vm.box = "ubuntu/xenial64"
    app.vm.network "private_network", ip: "192.168.10.100"
    app.hostsupdater.aliases = ["development.local"]
    app.vm.synced_folder "../Python-Sample-Application", "/home/ubuntu/app"
    app.vm.provision "chef_solo" do |chef|
      chef.add_recipe "python::default"
      chef.add_recipe "nginx::default"
    end


    # app.vm.synced_folder "environment/app", "/home/ubuntu/environment"
    # app.vm.provision "chef_solo" do |chef|
    #   chef.add_recipe "node::default"
    # end
    # app.vm.provision "shell", inline: set_var({"DB_HOST" => "192.168.10.101"}), privileged: false
  end

end
