## JJTech GCP CICD Project Runbook
### SonarQube Credentials
```
Token: jjtech-cicd-java-project: b456c2a171a25724547ec94e344f781724bb99ec
```
```
mvn sonar:sonar \
  -Dsonar.host.url=http://35.226.9.100:9000 \
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
ip address: 34.71.112.18:8081
```
### Maven Credentials
```
username: 
password: 
ip address: 34.68.62.149
```
### Ansible Credentials
```

```
### Jenkins Credentials
```
username: admin
password: admin
ip address: 34.68.62.149:8080
```
### GitHub Credentials
```
webhook: http://34.68.62.149:8080/github-webhook/
```