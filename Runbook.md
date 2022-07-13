## JJTech GCP CICD Project Runbook
### SonarQube Credentials
```
Token: jjtech-cicd-java-project: b456c2a171a25724547ec94e344f781724bb99ec
```
```
mvn sonar:sonar \
  -Dsonar.host.url=http://34.139.108.151:9000 \
  -Dsonar.login=b456c2a171a25724547ec94e344f781724bb99ec
```
```
sonarqube username: admin
sonarqube password: admin
```
### Nexus Credentials
```
username: admin
password: admin
ip address: 34.73.201.24:8081
Nexus Master encrypted password: Sb0WUMIN/+UH6NE2WQ0d2fOSH60jbBfWRPCuc33I0/Q=
Nexus Normal encrypted password: jJUCPqB9LxsHW2RR153vT3dwmaPIJl3I/WOufBTT8/w=
```
### Maven Credentials
```
username: 
password: 
ip address: 35.237.25.180
```
### Ansible Credentials
```

```
### Jenkins Credentials
```
username: admin
password: admin
ip address: 35.237.25.180:8080
```
### GitHub Credentials
```
webhook: http://35.237.25.180:8080/github-webhook/
```