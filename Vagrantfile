Vagrant.configure("2") do |config|
  # Use Ubuntu 22.04 (Jammy Jellyfish) as the base box
  config.vm.box = "ubuntu/jammy64"

  # Optional: Set up a private network
  config.vm.network "private_network", ip: "192.168.56.10"

  # Change the forwarded port to avoid conflicts
  config.vm.network "forwarded_port", guest: 80, host: 5678

  # Optional: Customize VM resources
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
    vb.cpus = 2
  end
end