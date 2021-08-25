Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-20.04"

  config.vm.synced_folder ".", "/vagrant"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "8192"
    vb.cpus = 4
  end

  config.vm.provision "shell", inline: <<-SHELL
    echo 'deb http://apt.llvm.org/focal/ llvm-toolchain-focal-12 main' > /etc/apt/sources.list.d/clang.list
    echo 'deb-src http://apt.llvm.org/focal/ llvm-toolchain-focal-12 main' > /etc/apt/sources.list.d/clang.list

    apt-get update
    apt-get install -y apache2 build-essential m4 openjdk-8-jdk libgmp-dev libmpfr-dev pkg-config flex bison z3 libz3-dev maven python3 cmake gcc zlib1g-dev libboost-test-dev libyaml-dev libjemalloc-dev python3-pip
    apt-get install -y clang-12 clang-tools-12 clang-12-doc libclang-common-12-dev libclang-12-dev libclang1-12 clang-format-12 clangd-12 lld-12

    python3 -m pip install graphviz

    curl -sSL https://get.haskellstack.org/ | sh
  SHELL

  config.vm.provision "shell", privileged: false, inline: <<-SHELL
    echo 'export PATH=/home/vagrant/.local/bin:$PATH' >> /home/vagrant/.bashrc

    git clone --recursive https://github.com/kframework/k.git
  SHELL
end
