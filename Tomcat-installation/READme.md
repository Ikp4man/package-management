#  **<span style="color:green">Ktech Academy, Lagos, London.</span>**
### **<span style="color:green">Contacts: +2347011045060<br> WebSite : <http://ktechacademy.net/></span>**
### **Email: kdevopsengineeringh@gmail.com**



## Apache Tomcat Installation And Setup In AWS EC2 Redhat Instance.
##### Prerequisite
+ AWS Acccount.
+ Create Redhat EC2 T2.micro Instance.
+ Create Security Group and open Tomcat ports or Required ports.
   + 8080 ..etc
+ Attach Security Group to EC2 Instance.
+ Install java openJDK 1.8+

### Install Java JDK 1.8+ 

``` sh
# install Java JDK 1.8+ as a pre-requisit for tomcat to run.
cd /opt 
sudo yum install git wget -y
sudo yum install java-1.8.0-openjdk-devel -y
# Download tomcat software and extract it.
sudo yum install wget unzip -y
```
### Install Apache Tomcat 9 Version 9.0.104, Apr 4 2025
``` sh
sudo wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.104/bin/apache-tomcat-9.0.104.tar.gz
sudo tar -xvf apache-tomcat-9.0.104.tar.gz    
sudo rm apache-tomcat-9.0.104.tar.gz    
sudo mv apache-tomcat-9.0.104 tomcat9
sudo chmod 777 -R /opt/tomcat9
sudo chown ec2-user -R /opt/tomcat9
sh /opt/tomcat9/bin/startup.sh
# create a soft link to start and stop tomcat
sudo ln -s /opt/tomcat9/bin/startup.sh /usr/bin/starttomcat
sudo ln -s /opt/tomcat9/bin/shutdown.sh /usr/bin/stoptomcat
sudo yum update -y
starttomcat
```

