Whenever we heard of a term known as firewall, the thing that first pops up in our mind is that where IP whitelisting happens or where we can either allow or block IP. So now what is firewall? Let's simplify it for all the domains of the world whether a person is aws cloud expert or azure cloud expert of gcp expert or any field who thinks that they do need a certification for validation of work inside this domain and if they belong to a particular set of domain, say aws, azure or gcp, they are the expert in that domain only. 

There is something known as pattern recognition inside DSA which is helpful for us to recognise patterns and solve problems accordingly to know in which direction can we think. Now, same happens in system design where our laptop has windows being installed where we are having firewall, similarly in cloud services, we have EC2 in AWS, VM in azure and compute engine in GCP which offers an OS where we can deploy our application.

Now, either our laptop or cloud's compute engines or VMs or EC2s have a specific IP allotted to it where one can run their applications, maybe we can play games on cloud instances or anything that we want to do. So, in our PC, we have certain applications that we use, for eg, VS Code, so we will see it inside inbound rules while microsoft edge or chrome inside outbound rules. So, why do they reside there? If we closely look into it, then we will observe that VS Code wants to access our server while inside edge or chrome, we want to search domains and perform operations over the internet, for which they are set as outbound rules.

Similar is the case in production. In prod, we have security groups in AWS EC2, NSG in Azure and VPC Firewall rules in GCP and basically these all act as a firewall for cloud but each are having different names. Now, for eg, I ssh into the EC2 instance or any instance using .pem file, firstly I need to define my SG properties as which port, ip and protocol is being allowed in inbound and outbound rules, so we all internet access to outbound rules and port 22, 80 and 443 respectively for ssh, http and https alongwith IP as inbound rules to access my server. Once we setup this configuration, then we have restricted port 80, 443 and 22 only to access our server while allowing access to the whole internet to access our application through outbound rules being set to All.

Now, since source and destination IP, source and destination ports, protocols are being involved, we can infer that firewall works on Layer 3/4 which is network layer and transport layer. So, here we have restricted the selective IPs to access our server by limiting inbound rules to only port 22 of ssh, 80 of http and 443 of https. Now, we use our .pem file to ssh into our server in order to scp our files so that we can deploy it over internet. In order to deploy the website over server, we need to setup a reverse proxy with the help of nginx to connect our server to the internet, where also comes the two type of proxies - forward proxy (not needed for server but needed for our laptop) and reverse proxy (not needed for our laptop but needed for our server).

The proxies work at application layer where we can set forward proxy in our laptop to connect at some specific port and allow only specific domains to be accessed through our laptop, while we can set reverse proxy inside the server to connect our application to the internet through nginx.













