# Getting Started - Observability from BIG-IP and NGINX
## Summary
The ELK(Elasticsearch, Logstash, Kibana) is the acronym for three open source projects. 
Elasticsearch is a search and analytics engine and Logstash is a server-side data processing pipeline that ingests data from multiple sources, transforms it and send to Elasticsearch.
Kibana let’s users visualize data with charts and graphs in Elasticsearch.
So we will use ELK to analyze app performance and visualize it on centralized dashboard to see/check easily correlation for N-S traffic and E-W traffic.<br>

![ELK_Topolgy](images/elk_topology.png)<br>


## Prerequisites
Here is needed to prepare an ELK stack server outside of the openshift cluster and you can refer this site ( https://www.digitalocean.com/community/tutorials/how-to-install-elasticsearch-logstash-and-kibana-elastic-stack-on-ubuntu-18-04 ) to install it and also see the logstash configuration ![file](./logstash.conf) used for this demo.


## Use case scenario
To achieve this scenario, UUID is generated by iRule on BIG-IP when traffic is arriving then it is inserting to http header. All of UUID with access logs are sending to ELK stack server then we can see what we want to see/check such as user location, response time by user location, response time BIG-IP and NGINX, etc.


## Setup and Configuration

1. Create HSL pool, iRule on BIG-IP
 We need to create pool with ELK stack server on BIG-IP then this pool member will be used by ![iRules](./iRules) to send access logs from BIG-IP to ELK stack.<br>
 
![ELK_Pool](images/elk_pool.png)
 
 The ELK server IP address is 10.69.33.1 and 8516 port is listening to get logs so pool service port should be 8516.<br>
![ELK_Pool](images/elk_pool_member.png)

 Then we need to create new VIP with bookinfo pool which created at previous case.<br>
![ELK_Pool](images/elk_vip.png)

 The new VIP name is a bookinfo-EdgeGW and the bookinfo pool is defined for default pool like below. The applied iRules name is elk_hsl_irule for this VIP so all of access logs will have the UUID and send to ELK server by this iRule.<br>
![ELK_Pool](images/elk_default_pool.png)

 Hereby, it’s ready to use ELK stack for BIG-IP access logs and next step is for apps in openshift cluster but we don’t need anything at the moment why it’s already pushed at the previous case in config-map.<br>
![ELK_Pool](images/elk_log.png)

2. Configure ELK server
 - will be updated


3. ELK Dashboard Sampels
![ELK_Pool](images/elk_map.png)


![ELK_Pool](images/elk_bigip.png)


![ELK_Pool](images/elk_response.png)


![ELK_Pool](images/elk_dot.png)



