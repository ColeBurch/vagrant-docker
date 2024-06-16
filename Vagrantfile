Vagrant.require_version ">= 2.2.6"


Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-22.04"

  host_port = 8000
  database_port = 5432
  host_ip_address = "127.0.0.1"

  POSTGRES_USER = "postgres"
  POSTGRES_PASSWORD = "password"
  DATABASE_NAME = "mydb"

  vm_num_cpus = 2
  vm_memory = 2048

  config.vm.define "postgres" do |postgres|
    postgres.vm.box = "bento/ubuntu-22.04"
    postgres.vm.hostname = "postgres"
    postgres.vm.network "forwarded_port", guest: 5432, host: 5432, host_ip: host_ip_address
    postgres.vm.provider "docker" do |d, override|
      override.vm.box = nil
      d.image = "postgres"
      d.name = "postgres"
      d.env = {
        POSTGRES_USER: POSTGRES_USER,
        POSTGRES_PASSWORD: POSTGRES_PASSWORD,
        POSTGRES_DB: DATABASE_NAME
      }
    end
  end

  config.vm.define "web" do |web|
    web.vm.box = "bento/ubuntu-22.04"
    web.vm.hostname = "web"
    web.vm.network "forwarded_port", guest: 8000, host: host_port, host_ip: host_ip_address
    web.vm.provider "docker" do |d, override|
      override.vm.box = nil
      d.build_dir = "./web"
      d.name = "web"
    end
  end

end
