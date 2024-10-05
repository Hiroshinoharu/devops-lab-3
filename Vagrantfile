Vagrant.configure("2") do |config|
  # Use the Arch Linux base box
  config.vm.box = "archlinux/archlinux"

  # Set up port forwarding (guest: 5000, host: 8080)
  config.vm.network "forwarded_port", guest: 5000, host: 8080

  # Provision the VM
  config.vm.provision "shell", inline: <<-SHELL
    # Update the package list and install necessary packages
    sudo pacman -Syu --noconfirm git nano vim python python-virtualenv python-pip

    # Create a virtual environment and install Flask
    python -m venv /home/vagrant/flask_venv
    source /home/vagrant/flask_venv/bin/activate
    pip install Flask
  SHELL

  # Upload the hello.py file to the VM
  config.vm.provision "file", source: "./hello.py", destination: "/home/vagrant/hello.py"

  # Run the Flask app
  config.vm.provision "shell", inline: <<-SHELL
    source /home/vagrant/flask_venv/bin/activate
    FLASK_APP=/home/vagrant/hello.py flask run --host=0.0.0.0
  SHELL
end
