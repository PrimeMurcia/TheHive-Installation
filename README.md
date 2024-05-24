--------------------------------------------------------------
                      TheHive 5 Installation Guide
--------------------------------------------------------------

1. **System Requirements:**
    - RAM: 8GB+ (16GB recommended)
    - HDD: 50GB+
    - OS: Ubuntu 22.04 LTS

2. **Installation Steps:**

   ```bash
   sudo su

Install Dependencies:

bash
Copy code
apt update && apt install -y \
wget gnupg apt-transport-https git ca-certificates \
ca-certificates-java curl software-properties-common \
python3-pip lsb-release
Install Java:

bash
Copy code
wget -qO- https://apt.corretto.aws/corretto.key | sudo gpg --dearmor -o /usr/share/keyrings/corretto.gpg
echo "deb [signed-by=/usr/share/keyrings/corretto.gpg] https://apt.corretto.aws stable main" | sudo tee -a /etc/apt/sources.list.d/corretto.sources.list
sudo apt update
sudo apt install -y java-common java-11-amazon-corretto-jdk
echo JAVA_HOME="/usr/lib/jvm/java-11-amazon-corretto" | sudo tee -a /etc/environment
export JAVA_HOME="/usr/lib/jvm/java-11-amazon-corretto"
Install Cassandra:

bash
Copy code
wget -qO -  https://downloads.apache.org/cassandra/KEYS | sudo gpg --dearmor -o /usr/share/keyrings/cassandra-archive.gpg
echo "deb [signed-by=/usr/share/keyrings/cassandra-archive.gpg] https://debian.cassandra.apache.org 40x main" | sudo tee -a /etc/apt/sources.list.d/cassandra.sources.list
sudo apt update
sudo apt install -y cassandra
Install Elasticsearch:

bash
Copy code
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo gpg --dearmor -o /usr/share/keyrings/elasticsearch-keyring.gpg
sudo apt-get install -y apt-transport-https
echo "deb [signed-by=/usr/share/keyrings/elasticsearch-keyring.gpg] https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-7.x.list
sudo apt update
sudo apt install -y elasticsearch
Install TheHive:

bash
Copy code
wget -O- https://archives.strangebee.com/keys/strangebee.gpg | sudo gpg --dearmor -o /usr/share/keyrings/strangebee-archive-keyring.gpg
echo 'deb [signed-by=/usr/share/keyrings/strangebee-archive-keyring.gpg] https://deb.strangebee.com thehive-5.2 main' | sudo tee -a /etc/apt/sources.list.d/strangebee.list
sudo apt-get update
sudo apt-get install -y thehive
Configuration:

Edit /etc/cassandra/cassandra.yaml:

cluster_name: 'your_cluster_name'
listen_address: your_ip_address
rpc_address: your_ip_address
-seed: "your_ip_address:7000"
Edit /etc/elasticsearch/elasticsearch.yml:

cluster.name: thehive
node.name: node-1
network.host: your_ip_address
http.port: 9200
cluster.initial_master_nodes: ["node-1"]
Start Services:

bash
Copy code
systemctl start cassandra
systemctl enable cassandra
systemctl start elasticsearch
systemctl enable elasticsearch
systemctl start thehive
systemctl enable thehive
Check Service Status:

bash
Copy code
systemctl status cassandra
systemctl status elasticsearch
systemctl status thehive
Additional Configuration (Optional):

Adjust permissions for TheHive directory:

bash
Copy code
chmod -R thehive:thehive /opt/thp
Edit TheHive configuration:

bash
Copy code
nano /etc/thehive/application.conf
Default Credentials:

Username: admin@thehive.local
Password: secret
