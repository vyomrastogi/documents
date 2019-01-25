## How to Install Elasticsearch
- install java jdk
  ` sudo yum install java-1.8.0-openjdk.x86_64 `
- install elasticsearch 6.x
  - Download and install the public signing key
    `rpm --import https://artifacts.elastic.co/GPG-KEY-elasticsearch`
  - Create a file `elasticsearch.repo` in `/etc/yum.repos.d` with content
```
[elasticsearch-6.x] 
name=Elasticsearch repository for 6.x packages
baseurl=https://artifacts.elastic.co/packages/6.x/yum
gpgcheck=1
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
enabled=1
autorefresh=1
type=rpm-md
```
 - install elasticsearch using command 
    `sudo yum install elasticsearch`
   - To setup auto start up at system reboot
      `sudo systemctl daemon-reload`
      `sudo systemctl enable elasticsearch.service`
  - update cluster.name
  - update data location in '/etc/elasticsearch/elasticsearch.yml'  to - ` /app/data/elastic/` [optional step]
  - update host and port details - ` host ipaddress and port (9200)`
  - node details
    - setup
      ```
      node.name
      node.data (true or false based on requirement)
      node.master(true or false based on requirement)
      node.ingest(true or false based on requirement)
      ```
  - update elasticsearch system configuration to set limitMEMLOCK to infinity, so that the process uses the memory limited by elasticsearch jvm configuration. 
  - configure jvm options at /etc/elasticsearch/jvm.options for -Xms1g -Xmx1g. Xms represents the initial size of total heap space and Xmx represents the maximum size of total heap space

#### How to start/stop Elasticsearch
  `sudo systemctl start elasticsearch.service`
  `sudo systemctl stop elasticsearch.service`

####Installation Directory
Config : `etc/elasticsearch/elasticsearch.yml`
Logs : `var/logs/elasticsearch/<log file>`
Default Data path : `var/lib/elasticsearch`

Different Configuration changes made during POC

path:
 logs: /var/log/elasticsearch
 data: /app/data/elastic


## How to Install Kibana
install kibana 6.x
Download and install the public signing key
`rpm --import https://artifacts.elastic.co/GPG-KEY-elasticsearch`
Create a file `kibana.repo` in `/etc/yum.repos.d` with content
```
[kibana-6.x]
name=Kibana repository for 6.x packages
baseurl=https://artifacts.elastic.co/packages/6.x/yum
gpgcheck=1
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
enabled=1
autorefresh=1
type=rpm-md
```
install kibana using `sudo yum install kibana`



