## Elasticsearch training lab

**Note**: This is forked from [georgebridgeman/elastic-practice-lab](https://github.com/georgebridgeman/elastic-practice-lab) and modified to suit my needs.

This is a simple lab environment for training and experimenting with Elasticsearch 7.4.0.

It will build nodes running on CentOS, and provision them with the required system settings to run Elasticsearch on a non-local IP. It's a naive method of provisioning but it's suitable for our requirements.

The lab is designed purely as a training tool. It doesn't use all the best practices for a production cluster and shouldn't be considered suitable for one.

If you are studying for Elastic Certified Engineer, or you've been on the Elasticsearch Engineer I and/or II courses, this lab will help you get familiar with the environment used in the exam and run the labs from the courses. The main difference is that we're using Vagrant here so need to run `vagrant ssh` instead of just `ssh`. If you would rather use SSH directly, you'll need to do some work to copy your public keys into the VMs.

### Dependencies
These four archives are required:
- [Elasticsearch 7.4.0](https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.4.0-linux-x86_64.tar.gz)
- [Kibana 7.4.0](https://artifacts.elastic.co/downloads/kibana/kibana-7.4.0-linux-x86_64.tar.gz)
- [Logstash 7.4.0](https://artifacts.elastic.co/downloads/logstash/logstash-7.4.0.tar.gz)
- [Filebeat 7.4.0](https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.4.0-linux-x86_64.tar.gz)

Logstash requires JDK, so make sure a JDK installer is downloaded.

The dataset files from the Elasticsearch Engineering 1 or 2 are required.

### Settings summary
- Each VM is given 1G RAM.
- Elasticsearch is configured (in `jvm.options`) with a 512M heap - [50% available RAM](https://www.elastic.co/guide/en/elasticsearch/reference/current/heap-size.html).
- The number of file descriptors [is increased](https://www.elastic.co/guide/en/elasticsearch/reference/current/file-descriptors.html).
- The number of threads [is increased](https://www.elastic.co/guide/en/elasticsearch/reference/current/max-number-of-threads.html).
- The `mmap` count limit [is increased](https://www.elastic.co/guide/en/elasticsearch/reference/current/vm-max-map-count.html).
- [Disable swapping](https://www.elastic.co/guide/en/elasticsearch/reference/current/setup-configuration-memory.html#swappiness)

### Running
- Install VirtualBox
- Install Vagrant
- Clone this repository
- Place 
	- the Elasticsearch archive into the `es_archive` folder
	- the Kibana archive into the `kb_archive` folder
	- the Logstash archive into the `ls_archive` folder
	- the Filebeat archive into the `fb_archive` folder
	- the JDK installer into the `jdk` folder
	- the Elasticsearch Engineer 1 or 2 dataset files into the `datasets` folder.	
- `cd` into the repo
- Run `vagrant up`

Without modifying `Vagrantfile`, Vagrant will spin up two VMs; one Elasticsearch node (`10.0.200.101`) and one instance of Kibana (`10.0.200.110`).

To start Elasticsearch, you can `vagrant ssh node1` and run `elasticsearch-7.4.0/bin/elasticsearch`. 

To start Kibana, you'll need to `vagrant ssh nodekb` and run `kibana-7.4.0/bin/kibana`. 

If you need more nodes, you can uncomment the provisioners for `node2` to `node7`, then run `vagrant up` again. When you start Elasticsearch on those nodes, they'll automatically join the cluster and shard reallocation will begin.

To ingest the datasets into Elasticsearch, you'll need to `vagrant ssh node1`, install the JDK, and then follow the instructions in local_lab.html (part of the Elasticsearch Engineer 1 and 2 materials). 

### Resetting
If you've been using the environment and want/need to burn everything down and start from scratch, you can use `vagrant destroy`. This will delete the VMs so the next time you `vagrant up`, you'll get a brand new cluster.
