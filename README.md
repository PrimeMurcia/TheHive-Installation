# TheHive Installation Guide

This guide provides step-by-step instructions to install TheHive on your system. Follow the steps below to set up TheHive along with its dependencies.

## Step 1: Download Dependencies

First, install the necessary dependencies:

```bash
sudo apt udpate
sudo apt install wget gnupg apt-transport-https git ca-certificates ca-certificates-java curl software-properties-common python3-pip lsb_release
Step 2: Install Java
Install Java using Amazon Corretto:
Add the Amazon Corretto GPG key:

bash
Copy code
wget -qO- https://apt.corretto.aws/corretto.key | sudo gpg --dearmor -o /usr/share/keyrings/corretto.gpg
Add the Corretto repository:

bash
Copy code
echo "deb [signed-by=/usr/share/keyrings/corretto.gpg] https://apt.corretto.aws stable main" | sudo tee -a /etc/apt/sources.list.d/corretto.sources.list
Update the package list:

bash
Copy code
sudo apt update
Install Java:

bash
Copy code
sudo apt install java-common java-11-amazon-corretto-jdk
Set JAVA_HOME environment variable:

bash
Copy code
echo JAVA_HOME="/usr/lib/jvm/java-11-amazon-corretto" | sudo tee -a /etc/environment export JAVA_HOME="/usr/lib/jvm/java-11-amazon-corretto"
Step 3: Verify Java Installation
Verify the Java installation by running:

bash
Copy code
java --version
You should see a result similar to:

arduino
Copy code
openjdk version "11.0.12" 2022-07-19 OpenJDK Runtime Environment Corretto-11.0.12.7.1 (build 11.0.12+7-LTS) OpenJDK 64-Bit Server VM Corretto-11.0.12.7.1 (build 11.0.12+7-LTS, mixed mode)
Step 4: Install Cassandra
Install Cassandra:
Add the Cassandra GPG key:

bash
Copy code
wget -qO - https://downloads.apache.org/cassandra/KEYS | sudo gpg --dearmor -o /usr/share/keyrings/cassandra-archive.gpg
Add the Cassandra GPG key:

bash
Copy code
echo "deb [signed-by=/usr/share/keyrings/cassandra-archive.gpg] https://debian.cassandra.apache.org 40x main" | sudo tee -a /etc/apt/sources.list.d/cassandra.sources.list # Update the package list
Update the package list:

bash
Copy code
sudo apt update
Install Cassandra:

bash
Copy code
sudo apt install cassandra
Step 5: Install Elasticsearch
Install Elasticsearch:
Add the Elasticsearch GPG key:

bash
Copy code
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo gpg --dearmor -o /usr/share/keyrings/elasticsearch-keyring.gpg
Install apt-transport-https:

bash
Copy code
sudo apt-get install apt-transport-https
Add the Elasticsearch repository:

bash
Copy code
echo "deb [signed-by=/usr/share/keyrings/elasticsearch-keyring.gpg] https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-7.x.list
Update the package list:

bash
Copy code
sudo apt update
Install Elasticsearch:

bash
Copy code
sudo apt install elasticsearch
Optional Elasticsearch Configuration
Create a jvm.options file under /etc/elasticsearch/jvm.options.d and add the following configurations:

diff
Copy code
-Dlog4j2.formatMsgNoLookups=true
-Xms2g
-Xmx2g
Step 6: Install TheHive
Install TheHive:
Add the StrangeBee GPG key:

bash
Copy code
wget -O- https://archives.strangebee.com/keys/strangebee.gpg | sudo gpg --dearmor -o /usr/share/keyrings/strangebee-archive-keyring.gpg
Add the StrangeBee repository:

bash
Copy code
echo 'deb [signed-by=/usr/share/keyrings/strangebee-archive-keyring.gpg] https://deb.strangebee.com thehive-5.2 main' | sudo tee -a /etc/apt/sources.list.d/strangebee.list
Update the package list:

bash
Copy code
sudo apt-get update
Install TheHive:

bash
Copy code
sudo apt-get install -y thehive
Accessing TheHive
TheHive will be accessible on port 9000 with the default credentials:

Username: admin@thehive.local
Password: secret
You can now navigate to http://<your-server-ip>:9000 to access TheHive.
