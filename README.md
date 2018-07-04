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
UN  10.0.4.41  82.83 KiB  8            100.0%            9b94bff6-1b37-4a54-ba27-097fe460b7b9  r1
UN  10.0.4.42  70.9 KiB   8            100.0%            35fed831-0b81-4012-a372-09d9404bf7f3  r1
UN  10.0.4.43  84.31 KiB  8            100.0%            020d1bc1-a965-47af-a6b0-7440ac1a92a3  r1
```

You can also check the Elasticsearch cluster status by running this command :

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
