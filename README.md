# Ansible : Playbook Elassandra

The aim of this project is to deploy a simple Elassandra cluster on Vagrant with some default configuration.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.

### Prerequisites

What things you need to run this Ansible playbook :

* [Vagrant](https://www.vagrantup.com/docs/installation/) must be installed on your computer
* Update the Vagrant file based on your computer (CPU, memory), if needed
* You must have download the ubuntu Xenial64 vagrant box :

```
vagrant box add https://app.vagrantup.com/ubuntu/boxes/xenial64
```

### Usage

A good point with Vagrant is that you can create, update and destroy all architecture easily with some commands.

Be aware that you need to be in the Vagrant directory to be able to run the commands.

#### Build Environment

Vagrant needs to init the project to run and build it :

```
vagrant up
```

After build, you can check which virtual machine Vagrant has created :

```
vagrant status
```

If all run like it is expected, you should see something like this :

```
$ vagrant status

Current machine states:

elassandra01                   running (virtualbox)
elassandra02                   running (virtualbox)
elassandra03                   running (virtualbox)
```

#### Deployment

To deploy the Elassandra cluster, you just have to run the Ansible playbook elassandra.yml with this command :

```
ansible-playbook elassandra.yml
```

If everything run as expected, you should connect to the server and check the status of Cassandra cluster with that command :

```
$ nodetool status
Datacenter: DC1
===============
Status=Up/Down
|/ State=Normal/Leaving/Joining/Moving
--  Address    Load       Tokens       Owns (effective)  Host ID                               Rack
UN  10.0.4.41  65.84 KiB  8            100.0%            5b40d7ba-7049-4165-b582-397e50fab2d0  r1
UN  10.0.4.42  82.76 KiB  8            100.0%            d7fff062-2be5-4013-8ef0-4a7899a2b8f2  r2
UN  10.0.4.43  65.84 KiB  8            100.0%            a5dcea5b-2aee-43bc-bfd9-e0760273a5c1  r3
```

You can also check the Elasticsearch instance status on each node by running this command :

```
$ curl "localhost:9200/_cluster/health?pretty"
{
  "cluster_name" : "Test Cluster",
  "status" : "green",
  "timed_out" : false,
  "number_of_nodes" : 1,
  "number_of_data_nodes" : 1,
  "active_primary_shards" : 1,
  "active_shards" : 1,
  "relocating_shards" : 0,
  "initializing_shards" : 0,
  "unassigned_shards" : 0,
  "delayed_unassigned_shards" : 0,
  "number_of_pending_tasks" : 0,
  "number_of_in_flight_fetch" : 0,
  "task_max_waiting_in_queue_millis" : 0,
  "active_shards_percent_as_number" : 100.0
}
```

#### Destroy

To destroy on what Vagrant has created, just run this command :

```
vagrant destroy
```

## Author

Member of Wikitops : https://www.wikitops.io/
