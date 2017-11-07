## What is Chef?
Chef is a system for automating the configuration of your provisioned infrastructure.  This could mean
anything from installing needed software packages to mounting a file system to
configuring a systemd service.  Chef (like Puppet, Ansible, and CFEngine) is an
implementation of [Promise Theory](https://en.wikipedia.org/wiki/Promise_theory).  In short, this means each resource defined in
a Chef recipe will end in a promised state or fail: *package x is installed*,
*postgresql.conf exists and has these properties set*, *directory x exists*.  Chef
also seeks to be idempotent, meaning you can call a resource over and
over again without changing its promised state (no conditionals needed).

## Structure
The basic unit is the resource.  A resource is a definition of desired state: *this file system should be mounted*, *this directory should be deleted/gone*.
The following is from the [community kafka cookbook](https://github.com/mthssdrbrg/kafka-cookbook)
```ruby
directory node['kafka']['config_dir'] do
  owner node['kafka']['user']
  group node['kafka']['group']
  mode '755'
  recursive true
end
```
This ruby block creates a directory using `node` variables (known as attributes)
to fill in the name, owner, and group.  You could also provide static strings instead
of using attributes
```ruby
directory '/etc/kafka/config' do
  owner 'kafka'
  group 'kafka'
  mode '755'
  recursive true
end
```
