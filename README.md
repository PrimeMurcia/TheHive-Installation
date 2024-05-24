--------------------------------------------------------------
  User Guide for Installing TheHive 5 on Ubuntu 22.04 LTS             
--------------------------------------------------------------

## Specifications
- **RAM**: 8GB+ (Recommend 16 GB)
- **HDD**: 50+ GB
- **OS**: Ubuntu 22.04 LTS

## Installing TheHive 5

### 1. Switch to Root User

```bash
sudo su
```


### 2. Install Dependencies

```bash
apt install wget gnupg apt-transport-https git ca-certificates ca-certificates-java curl software-properties-common python3-pip lsb-release
```


### 3. Install Java

```bash
wget -qO- https://apt.corretto.aws/corretto.key | sudo gpg --dearmor -o /usr/share/keyrings/corretto.gpg
echo "deb [signed-by=/usr/share/keyrings/corretto.gpg] https://apt.corretto.aws stable main" | sudo tee -a /etc/apt/sources.list.d/corretto.sources.list
sudo apt update
sudo apt install java-common java-11-amazon-corretto-jdk
echo JAVA_HOME="/usr/lib/jvm/java-11-amazon-corretto" | sudo tee -a /etc/environment
export JAVA_HOME="/usr/lib/jvm/java-11-amazon-corretto"
```


### 4. Install Cassandra

```bash
wget -qO - https://downloads.apache.org/cassandra/KEYS | sudo gpg --dearmor -o /usr/share/keyrings/cassandra-archive.gpg
echo "deb [signed-by=/usr/share/keyrings/cassandra-archive.gpg] https://debian.cassandra.apache.org 40x main" | sudo tee -a /etc/apt/sources.list.d/cassandra.sources.list
sudo apt update
sudo apt install cassandra
```


### 5. Install ElasticSearch

```bash
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo gpg --dearmor -o /usr/share/keyrings/elasticsearch-keyring.gpg
sudo apt-get install apt-transport-https
echo "deb [signed-by=/usr/share/keyrings/elasticsearch-keyring.gpg] https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-7.x.list
sudo apt update
sudo apt install elasticsearch

```


### Optional: Configure ElasticSearch

Create a jvm.options file under /etc/elasticsearch/jvm.options.d and add the following configurations:

```bash
-Dlog4j2.formatMsgNoLookups=true
-Xms2g
-Xmx2g
```

### 6. Install TheHive

```bash
wget -O- https://archives.strangebee.com/keys/strangebee.gpg | sudo gpg --dearmor -o /usr/share/keyrings/strangebee-archive-keyring.gpg
echo 'deb [signed-by=/usr/share/keyrings/strangebee-archive-keyring.gpg] https://deb.strangebee.com thehive-5.2 main' | sudo tee -a /etc/apt/sources.list.d/strangebee.list
sudo apt-get update
sudo apt-get install -y thehive
```

### 7. Configure Cassandra
Edit the cassandra.yaml file:

```bash
nano /etc/cassandra/cassandra.yaml
```

Set the following configurations:

```bash
cluster_name: 'your cluster name'  # e.g., PrimeSOC Project
listen_address: your ip address
rpc_address: your ip address
-seed: "your ip address:7000"
```

Save and exit.

Restart Cassandra:

```bash
systemctl stop cassandra.service
rm -rf /var/lib/cassandra/*
systemctl start cassandra.service
systemctl status cassandra.service
```


### 8. Configure ElasticSearch

Edit the elasticsearch.yml file:

```bash
nano /etc/elasticsearch/elasticsearch.yml
```

Set the following configurations:

```bash
cluster.name: thehive
node.name: node-1
network.host: your ip address
http.port: 9200
cluster.initial_master_nodes: ["node-1"]
```
Save and exit.

Start and enable ElasticSearch:

```bash
systemctl start elasticsearch
systemctl enable elasticsearch
systemctl status elasticsearch
```


