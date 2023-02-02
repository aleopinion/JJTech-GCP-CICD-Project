## JJTech GCP CICD Project Runbook
### SonarQube Credentials
```
Token: jjtech-cicd-java-project: b456c2a171a25724547ec94e344f781724bb99ec
```
### SonarQube Credentials to be used in Maven configuration => Below
```
mvn sonar:sonar \
  -Dsonar.host.url=http://35.231.101.201:9000 \
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
ip address: 34.139.33.2:8081
Nexus Master encrypted password: SS/+70MG8EoHpEaLw9XIs10BewaWW+vDYkBnYVtG7s8=
Nexus Normal encrypted password: J8WafLFt8MEHQYVQ9h7P6Jkj4RkhORk5mbs5E1Ol7e0=
```
### Maven Credentials
```
username: 
password: 
ip address: 35.243.159.225
```
### Ansible Credentials
```

```
### Jenkins Credentials
```
username: admin
password: admin
ip address: 35.243.159.225:8080
```
### GitHub Credentials
```
webhook: http://35.243.159.225:8080/github-webhook/
```