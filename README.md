# CI/CD Pipeline Practice — vProfile

A Jenkins CI/CD pipeline built on top of the vProfile reference application (Spring MVC/Security/JPA, Maven, JSP, MySQL) — used to practice a full build → test → code-quality → artifact-publish pipeline rather than to build the application itself.

## What this is

The application code (Spring MVC + MySQL account management app) is the standard vProfile training project used in DevOps CI/CD courses. My work here is the pipeline around it: a customized `Jenkinsfile` and supporting Ansible/userdata scripts for a self-hosted Jenkins → Nexus → SonarQube → Tomcat pipeline.

## Pipeline

```
Build (Maven) → Unit Test → Integration Test → SonarQube code analysis → Publish artifact to Nexus
```

`Jenkinsfile` stages:
- **Build** — `mvn clean install`, archives the resulting `.war`
- **Unit Test** / **Integration Test** — Maven test phases
- **Code Analysis** — SonarQube scan via `sonar-scanner`
- **Publish to Nexus** — uploads the versioned artifact to a Nexus repository

`userdata/` holds the provisioning scripts (`jenkins-setup.sh`, `nexus-setup.sh`, `sonar-setup.sh`) used to stand up each tool on its own EC2 instance, and `ansible/vprofile.yml` automates the deployment step.

## Prerequisites (application)

- JDK 8+, Maven 3+, MySQL 5.6+

## Database

```bash
sudo apt-get update && sudo apt-get install mysql-server
mysql -u <user_name> -p accounts < src/main/resources/db_backup.sql
```

## Tech Stack

Jenkins, Nexus, SonarQube, Ansible, Maven, Spring MVC/Security/JPA, MySQL, Tomcat.
