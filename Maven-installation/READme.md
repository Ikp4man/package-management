#  **<span style="color:green">Ktech Academy, Lagos, London.</span>**
### **<span style="color:green">Contacts: +2347011045060<br> WebSite : <http://ktechacademy.net/></span>**
### **Email: kdevopsengineering@gmail.com**



## Apache Maven Installation And Setup In AWS EC2 Redhat Instnace.
##### Prerequisite
+ AWS Acccount.
+ Create Redhat EC2 T2.medium Instnace with 4GB of RAM.
+ Create Security Group and open Required ports.
   + 22 ..etc
+ Attach Security Group to EC2 Instance.
+ Install java openJDK 1.8+

### Install Java JDK 1.8+  and other softares (GIT, wget and tree)

``` sh
# install Java JDK 1.8+ as a pre-requisit for maven to run.

sudo hostname maven
cd /opt
sudo yum install wget nano tree unzip git-all -y
sudo yum install java-17-openjdk-devel java-1.8.0-openjdk-devel -y
java -version
git --version
```

## 2. Download, extract and Install Maven
``` sh
#Step1) Download the Maven Software
sudo wget https://dlcdn.apache.org/maven/maven-3/3.9.9/binaries/apache-maven-3.9.9-bin.zip
sudo unzip apache-maven-3.9.9-bin.zip
sudo rm -rf apache-maven-3.9.9-bin.zip
sudo mv apache-maven-3.9.9/ maven
```
## .#Step3) Set Environmental Variable  - For Specific User eg ec2-user
``` sh
vi ~/.bash_profile  # and add the lines below
export M2_HOME=/opt/maven
export PATH=$PATH:$M2_HOME/bin
```
## .#Step4) Refresh the profile file and Verify if maven is running
```sh
source ~/.bash_profile
mvn -version
```

