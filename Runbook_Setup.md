**==============>>>>> Steps to set up Jenkins <<<<<====================**

**1 => Installs Java 1.8 or Java 8 or JDK on the Jenkins server. The reason is that Java is a core** 
**dependency for Jenkins. You cannot install Jenkins without setting  up Java. You must setup**
**Java for Jenkins to run. You could setup other versions, but it is always advisable to use the** 
**latest version because it has the lates bug fixes**
```
sudo yum install java-1.8* -y 
```

**2 => To install wget on the Jenkins server, because we need wget to download the specifc binary  file** 
**from the Jenkins repository which is hosted in the web. So, we will use wget to pull that binary** 
**file and proceed with the installation**
```
sudo yum install wget -y 
```

**3 => Jenkins will be intergrating with our source code manager which is Git. This integration is necessary** 
**because we have a solution called Webhook which is seated in Git and which plays the role of alerting**
**Jenkins whenever any developers change to the application is made available at the level of the**
**repository which is GitHub. Git is the soruce code manager. If we must ensure that there is communication** 
**between Git and Jenkins whenever a developer's change is made available at the sorce code repo, then we** 
**must install Git at the level of the Jenkins server**
```
sudo yum install git -y
```

**4 => Since we installed wget, we are going to use that utility at this level to pull the Jenkins binary**
**or actual Jenkins repository on the web. The file will be saved in the path '/etc/yum.repos.d/jenkins.repo'**
**which is shown on the terminal after running the command**
```
sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
```

**5 => To list or show the content of the Jenkins repo just downloaded using wget utility. Of the different** 
**files that were downloaded by the utility, you have 'jenkins.repo' which is now seated in our local** 
**server and meant to manage the Jenkins repository within this srver**
```
ls /etc/yum.repos.d/
```

**6 => To setup the specific keys for Jenkins. This command is not that important, but we are running it to**
**avoid breakage. The command is to set up SSL keys that Jenkins will be using - we are just importing them**
```
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
```

**7 => Recall the 'epel-release' repository that we dealt with before which houses most of the open source** 
**tools including Ansible. In most cases, you could go that route by pulling down that repository.**
**If Jenkins is there, then you will be able to install it. But if it is not there, that is when you** 
**can pull the other repository using command #4. So, this command is not mandatory, it is only when** 
**you want to use the 'epel-release' repository**
```
sudo yum install epel-release -y 
```

**8. We update the system so that we can have the latest libraries across the board for some of the things** 
**that we will be utilizing including Jenkins. Every repository that you have in your local including** 
**Jenkins repo that we just pulled down, if there are some particular binaries, libraries that may be,** 
**were recently added, it will go ahead and update all the repositories within your local machine.** 
**So, this command is just to update particular repos and softwares that exist within your local,** 
**which is this Jenkins server**
```
sudo yum update -y
```

**9. To install Jenkins within the server by making use of the Java utilities we doenloaded. With the Java-1.8.0,** 
**we are saying that during the time yum is performing this Jenkins installation, it should make use of the** 
**existing java utility, particularly Java 8 which is what we installed. The reason is because if you had java 1.7,** 
**Java 1.9 installed in here, yum will pick up any of those utilities. But if you want it to use a particular version,** 
**then you can specify that explicitely. But in our case, we could still leave it by taking out the Java-1.8 and it** 
**will still make use of Java-1.8 because that is the only version we have installed in the server**
```
sudo yum install jenkins java-1.8.0-openjdk-devel -y 
```

**10 => To Check the state or if Jenkins is actually installed using the 'systemctl' utility. It will tell** 
**you Jenkins is 'Inactive (dead)'. But we know it is installed. If you do not see anything or output,**
**it means something is wrong**
```
sudo systemctl status jenkins 
```

**11 => To Check the state or  if Jenkins is actually installed using the 'service' utility.** 
**It will tell you Jenkins is 'Inactive (dead)'**
```
sudo service jenkins status 
```

**11 => To start Jenkinks using the "systemctl" utility**
```
sudo systemctl start jenkins
```

**12 => To Start Jenkins using the "service" utility**
```
sudo service jenkins start
```

**13 => To Check the state of Jenkins**
```
sudo systemctl status jenkins
```

**14 => To enable jenkins so as to make it persistent, so that we do not have to be stoppping** 
**and starting Jenkins everytime we logout and start service again**
```
sudo systemctl enable jenkins
```

**15 => Port 8080 is the Jenkins application port #. Jenkins listens on port 8080. Takes you to the Jenkins**
**dashboard or User Interface (UI). If you do not see this dashboard, it means your Jenkins has not started**
**or you are missing something. By the time you get to this UI, you need to make use of 'administrative password'** 
**to get into Jenkins. And that admin password is saved in the location path displayed on the dashboard.** 
**You have to cat that path in order to get to the password. So, copy the path and go to your terminal and cat** 
**as shown in the nect command below**
```
http://external-ip:8080 
```

**16 => Using cat to expose the admin password of the Jenkins server. Copy the password,** 
**past on the Jenkins dashboard > Continue**
```
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

**17 => The administrative password for my Jenkins dashboard (backup project)**
```
cdfc5a0bbfbd4becada771dd2e360113 
```

**20 => The name for JDK when setting it up within Jenkins**
localJdk 

**21 => The Oracle Account details of Mbandi shown below for oue usage**
```
Oracle Account Credentials
```

**22 => Mbandi's Oracle account username**
```	
Username: mbandiawan@gmail.com
```

**23 => Mbandi's Oracle account password**
```
Password: JJTech@Accelerate2021
```

**24 => The name for Maven when setting up Maven within Jenkins**
```
localMaven 
```


**==============>>>>> Steps to set up SonarQube <<<<<====================**

**25 => To Install Java in the SonarQube Server. SonarQube heavily depends on Java, just like Jenkins** 
We will install Java before going ahead to install SonarQube**
```
sudo yum install java-1.8.0 -y
```

**26 => To install wget utility which will be used to download the specific repository that is used to manage SonarQube**
```
sudo yum install wget -y 
```

**27 => To use the wget utility to download the SonarQube repository. It will download the repository** 
**and save it in the path: /etc/yum.repos.d/**
```
sudo wget -O /etc/yum.repos.d/sonar.repo http://downloads.sourceforge.net/project/sonar-pkg/rpm/sonar.repo  
```

**28 => To view the just downloaded SonarQube repository**
```
ls /etc/yum.repos.d
```

**29 => To install SnarQube. This installation pulls all the different libraries and binaries from the** 
**repository that was just downloaded and setup in the local server. if we did not pull down that repository,** 
**this SonarQube installation will break.**
```
sudo yum install sonar -y 
```

**30 => To Start the SonarQube Service**
```
sudo service sonar start
```

**31 => To Enable SonarQube so that SonarQube can be persistent - when you stop and restart your server,** 
**SonarQube will remain started**
```
sudo systemctl enable sonar
```

**32 => To check the Status of SonarQube => "SonarQube is running" was displayed**
```
sudo service sonar status 
```

**33 => This command tells you some of the supported commands of the "service" utility**
```
sudo service sonar chkconfig
```

**--------------------------------------------------------------------------------------------------**
**34 => SonarQube Credentials => SonarQube Token generated for my practice section, with Token name = jjtech-cicd-java-project-practice.** 
**Actual Token details are stored in JJTech-GCP-CICD-Project directory in our Google-Cloud-Platform directory**
```
jjtech-cicd-java-project-practice: 
d4235f594ebe12a1d409adaa50706a63268c09b4 
```

**35 => Copied snippet from my practice SonarQube**
```
mvn sonar:sonar \
  -Dsonar.host.url=http://35.227.18.31:9000 \
  -Dsonar.login=d4235f594ebe12a1d409adaa50706a63268c09b4  
```
**-------------------------------------------------------------------------------------------------------**



**==============>>>>> Steps to set up Nexus <<<<<====================**

**36 => To update the centos vm**
```
sudo yum update -y 
```

**37. To Install Open JDK which is the same as Java in the Nexus Server. Nexus heavily depends on Java,** 
**just like Jenkins. We will install Java before going ahead to install Nexus**
```
sudo yum install java-1.8.0-openjdk.x86_64 -y 
```

**38 => To install wget on the Nexus server, because we need wget to download the specifc binary file** 
**from the Nexus repository which is hosted in the web. So, we will use wget to pull that binary** 
**file and proceed with the installation**
```
sudo yum install wget -y 
```

**39 => This command is to create a directory called "app" which will be inside "root". And when** 
**the directory is created, we also want to cd into it. So the && in the command simply means that** 
**after the first part of the command is executed, go ahead and execute the sencond part of it.So,** 
**when you want to run 2 commands sequentially, you make use of the && sign in linux. This directory /app** 
**will be used to house the binaries for Nexus which we are going to download. In there, we will unzip** 
**it and make use of it will all the other stuff that Nexus comes with in order to start it**
```
sudo mkdir /app && cd /app 
```

**40 => This command downloads the Nexus zipped file which will be seated in the /app directory.** 
**Since we already created and cd into the /app directory, so running this command from that directory**
**automaatically seats the file in that directory. Note that "Sonartype" still refers to Nexus in the**
**industry. Nexus is a product of Sonartype**
```
sudo wget -O nexus.tar.gz https://download.sonatype.com/nexus/3/latest-unix.tar.gz 
```

**41 => To confirm the downloaded file before unzipping it. The file is "nexus.tar.gz" which is the** 
**zipped file. It is still using the "tar" utility**
```
ls 
```

**42 => To unzip the nexus.tar.gz file and place everything in that parent directory /app. So the** 
**utility to unzip the file is "tar". Whenever you see "tar", know that you are unzipping. You can also** 
**use "tar" to zip a file**
```
sudo tar -xvf nexus.tar.gz 
```

**43 => To view the 2 unzipped files which are "nexus-3.40.1-01" and "sonartype-work"** 
```
ls   
```

**44 => To update or rename the Nexus unzipped file. The name is too long. We rename it to "nexus"**
**So we use the "mv" command to rename a file in linus**
```
sudo mv nexus-3.40.1-01 nexus
```

**45 => To confirm your new file after renaming**
```
ls  
```

**46 => There is one thing which is a little bit different when it comes to Nexus. When yo are performing**
**the arfact updload to Nexus including your Nexus setup within your local, starting and stoping Nexus, etc,** 
**you can set it as a "root" user or another user that has root pricileges. But as a root user,** 
**it not advisable. It is advisable to create a customized user to setup Nexus, because if someone** 
**gains acces to the Nexus processes that are running within your local machine, it will be a very big**
**issue in your environment. So, rather than giving root privileges, it is advisable to give regular user** 
**privileges. So that is what we are going to do. We are going to create a user and then, we will use** 
**that user to manage Nexus within this environment. So this command is to create a user called "nexus".**
**And this user will be in the home directory**
``` 
sudo adduser nexus OR sudo useradd nexus 
```

**47 => To list the users in the home directory so as to check if the newly created user is there**
```
ls /home 
```

**48 => To list the "creator" and "owner" of the nexus file that we downloaded, unzipped and renamed.**
**And it shows up as "root" and "root".Therefore, if you use any other user to manage that nexus**
**file the way it at this moment, seeing that "root" is the "creator" and the "owner" of the nexus file,** 
**that process will or fail. Now since we ceated a user called "nexus", we are going to update or change** 
**the "creator" and "ownership" of that nexus file to be pointing at that "nexus" user we just created,** 
**becuase that is the user that we want to use to manage the nexus processcess within this environment** 
**or within this pipeline**
```
ls -al
```

**49 => This command changes the creator and ownership of the nnexus file from root and root to nexus** 
**and nexus. "sudo chown -R" allows you to change a directory's or file's creator and ownership. Where you have** 
**"nexus:nexus nexus", you are saying that you are changing the creator and ownership of nexus file** 
**from "root" and "root" to "nexus" and "nexus". You want to do this so that the user will be able to** 
**manage the file without making use of "sudo" or needing "root level privileges"**
```
sudo chown -R nexus:nexus nexus 
```

**50 => To re-confirm the "creator" and "owner" of the nexus file after the update**
```
ls -al
```

**51 => To also change the creator and owner of the sonatype-work file which was downloaded and unzipped** 
**with the nexus file from "root" and "root" to "nexus" and "nexus"**
```
sudo chown -R nexus:nexus sonatype-work 
```

**52 => To confirm the new creator and the owner of the "sonatype-work" file**
```
ls -al
```

**53 => To cd into nexus and into bin directory, and then list the content of bin directory.**
**In the bin directory, there are 2 important files- the "nexus" file and the "nexus.rc" file.**
**The nexus file is used to start and stop the nexus service while the nexus.rc file is used to**
**manage the user that will be ued to start and stop nexus. So we need to vi into the nexus.rc**
**file to update that file**
```
cd nexus && cd bin && ls
```

**54. To vi into the nexus.rc file and update the file. Since we created a user called "nexus",**
**we need to pass the user to this file so the system can identify the user that will be used to** 
**manage nexus in this environment and in the entire pipeline. #run_as_user=""  updated to run_as_user="nexus"**
```
sudo vi  nexus.rc
```

**55 => Absolute path to the same location as above**
```
sudo vi  /app/nexus/bin/nexus.rc 
```

**56 => Specifies the directories which houses files that are used to manage particular services** 
**which you can use the service or systemctl utility or cammand to start and stop. We need to also**
**create the same thing for nexus because at the moment, there is no such nexus service utility** 
**within this directory. So we need to create it**
```
ls /etc/systemd/system 
```

**57. To check the status of Nexus before we create and update the service file for Nexus.** 
**The command will fail because the file does not exit yet**
```
sudo systemctl status nexus
```

**58 => To create and update the service utility for nexus and place in the directories for**
**all the service and systemctl service files.The name of the file is called "nexus.service".**
**Copy and paste the parameters below, save and quit**
```
sudo vi /etc/systemd/system/nexus.service  
```

**-------------------------------------------------------**
```
[Unit] 
Description=nexus service
After=network.target 
	
[Service]
Type=forking 
LimitNOFILE=65536 
User=nexus 
Group=nexus 
ExecStart=/app/nexus/bin/nexus start
ExecStop=/app/nexus/bin/nexus stop 
User=nexus 
Restart=on-abort 
	
[Install] 
WantedBy=multi-user.target
```
**---------------------------------------------------------**

**59 => To chect the status of Nexus after ceating the serice file => Active: inactive (dead)**
```
sudo systemctl status nexus 
```

**60 => To start the Nexus service**
```
sudo systemctl start nexus 
```

**61 => To re-check the status of Nexus service => Active: active (running)**
```
sudo systemctl status nexus
```

**62 => To enable the Nexus service and make it persistent**
```
sudo systemctl enable nexus
```

**63 => The path where you have the Nexus password**
```
/app/sonatype-work/nexus3/admin.password 
```

**64 => To get the password for Nexus**
```
sudo cat /app/sonatype-work/nexus3/admin.password
```

**65 => Nexus admin password => My Practice**
```
d42f5fda-05ff-48b5-94eb-589c0ea56d5a 
```

**66 => When you setup Webhook within your project in Github**
```
http://IP of Jenkins instance:8080/github-webhook/ 
``` 

**67 => When you setup Webhook within your project in Github....also captured in Runbook.md**
```
http://35.237.25.180:8080/github-webhook/
```


