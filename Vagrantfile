# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

ENV['VAGRANT_DEFAULT_PROVIDER'] ||= 'docker'

# we require defaults
if ! ENV.has_key?("PLEX_SETUP")
  puts 'required environment variables not setup, please source defaults'
  exit 1
end

# setup environment variables
env_config = {}
ENV.each do |k, v|
  if k.match(/^PLEX/)
    env_config[k] = v
  end
end

Vagrant.configure("2") do |config|
  config.vm.define "plex" do |v|
    v.vm.provider "docker" do |d|
      d.ports = ["32400:32400/tcp", "1900:1900/udp", "5353:5353/udp", "32410:32410/udp", "32412:32412/udp", "32413:32413/udp", "32414:32414/udp", "32469:32469/tcp"]
      d.build_dir = "./plex"
      d.name = "plex"
      d.env = env_config
      d.volumes = ["#{env['PLEX_SHARE']}:/media/"]
    end
  end
end
