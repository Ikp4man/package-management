#  **<span style="color:green">Ktech Academy, Lagos, London.</span>**
### **<span style="color:green">Contacts: +2347011045060<br> WebSite : <http://ktechacademy.net/></span>**
### **Email: kdevopsengineering@gmail.com**



## SonarQube Installation And Setup In AWS EC2 Redhat Instance.
##### Prerequisite
+ AWS Acccount.
+ Create Redhat EC2 T2.medium Instance with 4GB RAM.
+ Create Security Group and open Required ports.
   + 9000 ..etc
+ Attach Security Group to EC2 Instance.
+ Install java openJDK 1.8+ for SonarQube version 7.8

## 1. Create sonar user to manage the SonarQube server
```sh
#As a good security practice, SonarQuber Server is not advised to run sonar service as a root user, 
# create a new user called sonar and grant sudo access to manage sonar services as follows

sudo useradd sonar
# Grand sudo access to sonar user
sudo echo "sonar ALL=(ALL) NOPASSWD:ALL" | sudo tee /etc/sudoers.d/sonar
sudo hostname sonar
#sudo passwd sonar
sudo su - sonar
```
## 2. Enable PasswordAuthentication in the server
```sh
sudo sed -i "/^[^#]*PasswordAuthentication[[:space:]]no/c\PasswordAuthentication yes" /etc/ssh/sshd_config
sudo service sshd restart
```
### 3. Install Java JDK 1.8+ required for sonarqube to start

``` sh
cd /opt
sudo yum -y install unzip wget git
sudo wget -c --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u131-b11/d54c1d3a095b4ff2b6607d096fa80163/jdk-8u131-linux-x64.rpm
sudo yum install jdk-8u131-linux-x64.rpm -y
```
### 4. Download and extract the SonarqQube Server software.
```sh
sudo wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-7.8.zip
sudo unzip sonarqube-7.8.zip
sudo rm -rf sonarqube-7.8.zip
sudo mv sonarqube-7.8 sonarqube
```

## 5. Grant file permissions for sonar user to start and manage sonarQube
```sh
sudo chown -R sonar:sonar /opt/sonarqube/
sudo chmod -R 775 /opt/sonarqube/
```
### 6. start sonarQube server
```sh
sh /opt/sonarqube/bin/linux-x86-64/sonar.sh start 
sh /opt/sonarqube/bin/linux-x86-64/sonar.sh status
```

### 7. Ensure that SonarQube is running and Access sonarQube on the browser
# sonarqube default port is = 9000
# get the sonarqube public ip address 
# publicIP:9000
```sh
curl -v localhost:9000
54.236.232.85:9000
default USERNAME: admin
default password: admin
```
New installation script updated 2025

#!/bin/bash

# 1. Create a sonar user
sudo useradd -m -d /opt/sonarqube -s /bin/bash sonar

# 2. Grant sudo access to sonar user without requiring a password
echo "sonar ALL=(ALL) NOPASSWD:ALL" | sudo tee /etc/sudoers.d/sonar

# 3. Optionally, set the hostname (skip if not needed)
sudo hostnamectl set-hostname sonar

# 4. Install required packages
sudo apt update
sudo apt install -y unzip wget git openjdk-17-jdk openjdk-8-jdk

# 5. Switch to /opt directory for installing SonarQube
cd /opt
----------------------------------------------------------------------------------------
#sudo wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-2025.1.zip
-------------------------------------------------------------------------------------------
# 6. Download and extract SonarQube 7.8 (use a newer version if needed)
sudo wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.9.6.92038.zip
sudo unzip sonarqube-9.9.6.92038.zip
sudo rm -rf sonarqube-9.9.6.92038.zip
sudo mv sonarqube-9.9.6.92038 sonarqube       

# 7. Grant permissions to sonar user for managing SonarQube
sudo chown -R sonar:sonar /opt/sonarqube/
sudo chmod -R 775 /opt/sonarqube/

# 8. Start SonarQube as sonar user
sudo su - sonar -c "sh /opt/sonarqube/sonarqube-9.9.6.92038/bin/linux-x86-64/sonar.sh start"

# 9. Check the status of SonarQube
sudo su - sonar -c "sh /opt/sonarqube/sonarqube-9.9.6.92038/bin/linux-x86-64/sonar.sh status"

echo "SonarQube installation complete. Access it via http://<your-server-ip>:9000"
