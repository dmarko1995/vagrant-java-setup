Vagrant.configure("2") do |config|
  # Використовуємо образ Ubuntu 22.04
  config.vm.box = "ubuntu/jammy64"

  # Налаштування приватної мережі
  config.vm.network "private_network", ip: "192.168.100.100"

  # Налаштування ресурсів (2 CPU, 4GB RAM)
  config.vm.provider "virtualbox" do |vb|
    vb.cpus = 2
    vb.memory = "4096"
  end

  # Встановлення Java 17
  install_deps = <<-SHELL
    sudo apt update
    sudo apt install -y openjdk-17-jdk
  SHELL

  # Виконуємо shell-скрипт
  config.vm.provision "shell", inline: install_deps

  # Тригер для запуску Gradle після підняття віртуальної машини
  config.vm.provision "trigger" do |trigger|
    trigger.name = "Start Application"
    trigger.run = { "inline" => "cd /vagrant && ./gradlew bootRun" }
  end
end
