# CI/CD Pipeline Practice — vProfile

A Jenkins CI/CD pipeline built on top of the vProfile reference application (Spring MVC/Security/JPA, Maven, JSP, MySQL) — used to practice a full build → test → code-quality → artifact-publish pipeline rather than to build the application itself.

## What this is

This repository is a copy of the **vProfile** DevOps course project, used to practise a Jenkins -> Nexus -> SonarQube -> Tomcat CI/CD pipeline on EC2 instances. It is a learning exercise, not an original application or pipeline design.

## Credits and attribution

- The application code, `Jenkinsfile`, `ansible/vprofile.yml`, the `userdata/` provisioning scripts and the commit history before 2026 come from the upstream vProfile project, published by **devopshydclub / Visualpath** (see [devopshydclub/vprofile-project](https://github.com/devopshydclub/vprofile-project)); that history lists contributors including Wahid Khan and Imran Teli. They are credited here as the authors of that work.
- No licence file is included in this repository; check the upstream project for its terms before reusing the code.
- The only change recorded in this repository's history under my account is the rewrite of this README. Any local modifications I made while following the course are not separately tracked here.

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
