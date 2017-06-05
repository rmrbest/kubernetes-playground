Vagrant.require_version '>= 1.6.0'
VAGRANTFILE_API_VERSION = '2'
ENV['VAGRANT_DEFAULT_PROVIDER'] = 'docker'

require 'yaml'

containers = YAML.load_file(File.join(File.dirname(__FILE__), 'containers.yml'))

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.provider 'docker' do |docker|
    docker.vagrant_vagrantfile = 'VagrantfileHost'
  end # config.vm.provider

  # Iterate through the entries in the YAML file
  containers.each do |container|
    config.vm.define container['name'] do |cntnr|

      # Disable synced folders for the Docker container
      # (prevents an NFS error on "vagrant up")
      cntnr.vm.synced_folder '.', '/vagrant', disabled: true

      # Configure the Docker provider for Vagrant
      cntnr.vm.provider 'docker' do |docker|

        # Specify the Docker image to use, pull value from YAML file
        docker.image = container['image']
        docker.build_dir = container['build_dir']
        # Specify port mappings, pull value from YAML file
        # If omitted, no ports are mapped!
        docker.ports = container['ports']
        docker.volumes = container['volumes']
        # Specify a friendly name for the Docker container, pull from YAML file
        docker.name = container['name']
      end # contnr.vm.provider
    end # config.vm.define
  end # containers.each
end # Vagrant.configure
