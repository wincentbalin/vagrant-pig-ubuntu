# -*- mode: ruby -*-
# vi: set ft=ruby :

PIG_VERSION = "0.15.0"
PIG_DIR = "pig-#{PIG_VERSION}"
PIG_FILE = "#{PIG_DIR}.tar.gz"
PIG_URL_DIR = "http://www.eu.apache.org/dist/pig/latest"
PIG_URL = "#{PIG_URL_DIR}/#{PIG_FILE}"
PIG_LOCAL_DIR_PARENT = "/opt"
PIG_LOCAL_DIR = "#{PIG_LOCAL_DIR_PARENT}/pig"
PIG_LOCAL_DIR_BIN = "#{PIG_LOCAL_DIR}/bin"
PIG_LOCAL_DIR_OLD = "#{PIG_LOCAL_DIR}.old"
PIG_LOCAL_DIR_NEW = "#{PIG_LOCAL_DIR_PARENT}/#{PIG_DIR}"
PIG_TMP_FILE = "/tmp/#{PIG_FILE}"

Vagrant.configure(2) do |config|
  config.vm.box = "hashicorp/precise64"

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get -y install openjdk-7-jdk
    apt-get -y install htop vim
    echo Downloading Pig...
    wget -q -O #{PIG_TMP_FILE} #{PIG_URL}
    echo Installing Pig...
    if [ -d #{PIG_LOCAL_DIR} ]
    then
      rm -rf #{PIG_LOCAL_DIR_OLD}
      mv #{PIG_LOCAL_DIR} #{PIG_LOCAL_DIR_OLD}
    fi
    tar zxf #{PIG_TMP_FILE} -C #{PIG_LOCAL_DIR_PARENT}
    mv #{PIG_LOCAL_DIR_NEW} #{PIG_LOCAL_DIR}
    rm #{PIG_TMP_FILE}
    echo Setting JAVA_HOME variable...
    echo >> ~vagrant/.bashrc
    echo '# Enable Apache Pig' >> ~vagrant/.bashrc
    echo "export JAVA_HOME=$(readlink -f /usr/bin/java | sed \"s:bin/java::\")" >> ~vagrant/.bashrc
    echo 'export PATH=$PATH:#{PIG_LOCAL_DIR_BIN}' >> ~vagrant/.bashrc
  SHELL
end
