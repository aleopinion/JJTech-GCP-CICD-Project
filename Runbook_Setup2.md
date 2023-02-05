**Webhook address linking and alerting Jenkins from Git**
```
http://jenkinspublicip:8080/github-webhook/ 
```
```
http://35.243.159.225:8080/github-webhook/
```



**1.The default location where the .war file is stored after build before Maven pickes**
**it and shares or stores in any distributed or centralized artifactory for better**
**integration of other tools with the artifact**
```
/var/lib/jenkins/workspace/JJtech-CICD-Java-Project-Pipeline/webapp/target/webapp.war ===> 
```


**=========>>>>>>>>>>>>>> Maven setup <<<<<<<<<<<=======================**

**1 => To download the Maven repository since we are setting up Maven on top of the server.**
**We did not have to install wget utility since we already have it installed in the server**
**during Jenkins setup. The repository has all the binaries and libraries to set up Maven in** 
**this environment. The Maven repository download "epel-apache-maven.repo" is stored in the**
**path "/etc/yum.repos.d/epel-apache-maven.repo"**
```
sudo wget https://repos.fedorapeople.org/repos/dchen/apache-maven/epel-apache-maven.repo -O /etc/yum.repos.d/epel-apache-maven.repo 
```

**2 => This command helps to make some changes within the repo. The main thing here is the "sed"**
**command. The "sed" command is used to update files or objects in Linux without getting into**
**the files or objects. We are here using it to setup some parameters**
```										
sudo sed -i s/\$releasever/6/g /etc/yum.repos.d/epel-apache-maven.repo
```

**3 => To call Maven from the downloaded repository and installing Apache-Maven**
```
sudo yum install -y apache-maven 
```
 
**4 => To create and encrypt the nexus admin password which is also saved in the Runbook.md file**
```
mvn -emp admin 
```
 
**5 => To switch to root**
```
sudo su 
```

**6 => Change directory to the root directory**
```
cd /
```

**7 => To list all the sub-directories within the root directory**
```
ls 
```

**8 => To cd into the root directory that is within the main root directory**
```
cd root 
```

**9 => To create the directry called .m2**
```
mkdir .m2
```

**10 => To list all the hidden directories**
```
ls -a 
```

**11 => To cd into the .m2 directory**
```
cd .m2 
```

**12 => To create and vi into the settings-security.xml file for updating**
```
vi settings-security.xml 
```

**13 => Copy the block of code below and paste in the settings-security.xml file. Save and exit**
```
<?xml version="1.0"?>
<settingsSecurity>
   <master>{admin}</master>
</settingsSecurity>
```

**14 => To create and encrypt the normal password for Nexus which is also saved in the Runbook.md file**
```
mvn -ep admin 
```

**15 => To create and vi into the settings.xml file for editing**
```
vi settings.xml 
```

**16 => Copy the block of code below and paste in the settings.xml file. Save and exit**
```
	<?xml version="1.0" encoding="UTF-8"?>
	
	<settings xmlns="http://maven.apache.org/POM/4.0.0"
	        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	          xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd">
	
	  <localRepository>/var/lib/jenkins/.m2/repository</localRepository>
	
	<servers>
	   <server>
	        <id>nexus</id>
	        <username>admin</username>
	        <password>{admin}</password>
	    </server>
	</servers>
	
	<mirrors>
	    <mirror>
	      <id>nexus</id>
	      <name>nexus</name>
	      <url>http://13.235.132.119:8081/repository/maven_project/</url>
	      <mirrorOf>*</mirrorOf>
	    </mirror>
	  </mirrors>
	
	</settings>
```

**17 => To see that the update was effective**
```
cat settings-security.xml
```

**18 => To see that the update was effective**
```
cat settings.xml 
```

**19 => To move the file to the location where Maven will identify and utilize the file**
```
mv settings-security.xml /var/lib/jenkins/.m2 
```

**20 => To move the file to the location where Maven will identify and utilize the file**
```
mv settings.xml /var/lib/jenkins/.m2 
```

**21 => To list the files in the .m2 files just to confirm hat the files were actually moved over**
```
ls /var/lib/jenkins/.m2 
```

**22 => To cd in the .m2 directory**
```
cd /var/lib/jenkins/.m2 
```

**23 => To view the level of ownership and permissions of the files just created**
```
ls -al 
```

**24 => To change ownership/reator of the file to jenkins/jenkins**
```
chown jenkins:jenkins settings.xml 
```

***25 => To change ownership/reator of the file to jenkins/jenkins**
```
chown jenkins:jenkins settings-security.xml 
```

**26 => To Assign full "User" permission, read and exexute permissions for "Group" and "Others"**
```
chmod 755 settings.xml settings-security.xml  
```


**=======>>>>>>>>>Ansible setup on the Jenkins/Maven/Ansible sever starts from here <<<<======**

**27 => To install Ansible on the Ansible server**
```
sudo yum install ansible -y 
```

**28 => To create a user called ansadmin**
```
sudo useradd ansadmin 
```

**29 => To create a password for user ansadmin which is also = ansadmin**
```
sudo passwd ansadmin 
```

**30 => cd ansible directory**
```
cd /etc/ansible/ 
```

**31 => To list the components of the Ansible directory**
```
ls 
```

**32 => To vi into and update the ansible.cfg particularly the "host_key_checking" line** 
**of code within the file so that when Ansible tries to log in automatically with the**
**username and password, the server will not request Ansble to figerprint by typing "yes"** 
**before granting that access**
```
sudo vi ansible.cfg 
```

**33 => To take you to the exact location to update
```
:/host_key_checking 
```
```
/host_key_checking
```

**33 => To vi into the host file and supply the Ansible "hosts" file the IP addrresses of**
**the Client nodes that we want Ansible to manage or perform that deployment in. In this case,** 
**the DEV and the Prod instances are the client servers**
```
sudo vi hosts 
```
```
[prod]
internalIP ansible_user=ansadmin ansible_password=ansadmin 
[dev]
internalIP ansible_user=ansadmin ansible_password=ansadmin
```
```
[prod]
10.142.0.5 ansible_user=ansadmin ansible_password=ansadmin 
[dev]
10.142.0.6 ansible_user=ansadmin ansible_password=ansadmin
```


**=========>>>>>>>>>>dev and prod setup <<<<<<<<<========**

**34 => To create common username called ansadmin in the client instance**
```
sudo useradd ansadmin 
```

**35 => To create a password for the common username called ansadmin (same as user name)**
```
sudo passwd ansadmin 
```

**36 => To vi and update the sshd_config file for password authentication**
```
sudo vi /etc/ssh/sshd_config 
```

**37 => To take you to the exact location to update**  
```
:/PasswordAuthentication 
```

**38 => To restart service so that the config update can take effect**
```
sudo service sshd restart
```

**39 => To update the sudoers file for user authorization**
```
sudo vi /etc/sudoers 
```

**40 => To take you to the exact location to update** 
```
:/wheel or /wheel 
```

**41. To add the user to the authorization file**
```
sudo usermod -aG wheel ansadmin
```

**42 => To see that the sudoers file accepted the update**
```
sudo cat /etc/sudoers 
```

**43 => To update the client instance with the latest packages (binaries and libraries)** 
**before installing apache tomcat, since apache tomcat needs the latest binaries to function properly**
```
sudo yum update -y 
```

**44 => Tried installing tomcat8.5 but was not successful**
```
sudo yum install tomcat8.5 -y 
```

**45 => Installed tomcat**
``` 
sudo yum install tomcat -y 
```

**46 => To start tomcat**
```
sudo systemctl start tomcat
```

**47 => To enable tomcat so that tomcat can be persistent**
```
sudo systemctl enable tomcat 
```

**48 => To check the status of tomcat**
```
sudo systemctl status tomcat
```
**======>>>>>>>>>>>>>> End of dev and prod setup <<<<<===========**



**----------------------------------------------------------------------------------------------**
**WE COULD NOT ACCESS THE APLICATION ON THE BROWSER FROM THE DEV INSTANCE, ALTHOUGH THE DEPLOYMENT** 
**TO DEV ENVIRONMENT WAS A SUCCESSFUL. SO, MBANDI TRIED TO RE-INSTALL THE APACHE TOMCAT, THINKING**
**THAT THE VERSION WE INSATLLED COULD BE THE ISSUE**


