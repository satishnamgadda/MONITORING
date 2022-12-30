-------------------------------------
# types of logs
Types of Logs
Nearly every component in a network generates a different type of data and each component collects that data in its own log. Because of that, many types of logs exist, including:

Event Log: a high-level log that records information about network traffic and usage, such as login attempts, failed password attempts, and application events.
Server Log: a text document containing a record of activities related to a specific server in a specific period of time.
System Log (syslog): a record of operating system events. It includes startup messages, system changes, unexpected shutdowns, errors and warnings, and other important processes. Windows, Linux, and macOS all
generate syslogs.
Authorization Logs and Access Logs: include a list of people or bots accessing certain applications or files.
Change Logs: include a chronological list of changes made to an application or file.
Availability Logs: track system performance, uptime, and availability.
Resource Logs: provide information about connectivity issues and capacity limits.
Threat Logs: contain information about system, file, or application traffic that matches a predefined security profile within a firewall.
--------------------------------------------
         APACHE APP MONITORING

# create a Elastic Cloud Account (elastic.cloud.io) 
# a 14 day free trail
first create a deployment
goto  > Manage this Deployment
get the ElasticSearch Endpoint        
![preview](/Images/monitoring11.png)
goto  > Manage this Deployment > security
# get user & password
    user: elastic
    passwd: <password>
![preview](/Images/monitoring12.png)

# check the Response from Elsticcloud, Run the following
curl -u <user>:<password> <elasticsearch- EndPoint>
![preview](/Images/monitoring1.png)

# create linux vm ubuntu,
# install apache
sudo apt update
sudo apt install apache2 -y 
curl http://localhost
![preview](/Images/monitoring2.png)

# install metricBeat on ubuntu using APT
https://www.elastic.co/guide/en/beats/metricbeat/current/metricbeat-installation-configuration.html

wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
sudo apt-get install apt-transport-https
echo "deb https://artifacts.elastic.co/packages/8.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-8.x.list
sudo apt-get update && sudo apt-get install metricbeat
sudo systemctl enable metricbeat

# Specify the cloud.id of your Elasticsearch Service, and set cloud.auth to a user who is authorized to set up Metricbeat. we have to configure in /etc/metricbeat/metricbeat.yml
sudo vi /etc/metricbeat/metricbeat.yml
![preview](/Images/monitoring3.png)
sudo metricbeat modules list
sudo metricbeat modules enable apache
sudo metricbeat setup -e
sudo systemctl enable metricbeat.service
sudo systemctl start metricbeat.service
# goto elastic-cloud > navigate to Discover 
#                     > navigate to Dashboard
![preview](/Images/monitoring4.png)
![preview](/Images/monitoring5.png)
