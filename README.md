# ReleaseManagerChallengeG
Release Manager Challenge

## Pre requisites

- ansible

  For MacOS: `brew install ansible`

- vagrant

  For MacOS: `brew cask install vagrant`

- virtualbox

  For MacOS: `brew cask install virtualbox`

## Overview

This setup deploys the required infrastructure and components to run TimeOff.Management application in a CI/CD environment. 
  
**Required Infrastructure - Deployment Diagram**
![Required Infrastructure - Deployment Diagram](https://github.com/nat55555/ReleaseManagerChallengeG/blob/master/docs/images/deployment-diagram.png)  
  
**Application CI/CD Configuration**
![Application CI/CD Configuration](https://github.com/nat55555/ReleaseManagerChallengeG/blob/master/docs/images/ci-cd-diagram.png)  
  
For details about the TimeOff.Management application, refer to the application's [Readme](https://github.com/nat55555/timeoff-management-application/blob/master/README.md) file 

## Base files

Clone the gitlab ReleaseManager Resources

```bash
git clone https://github.com/nat55555/ReleaseManagerChallengeG.git ReleaseManagerChallengeG
cd ReleaseManagerChallengeG
```

The downloaded resources of interest should be in the following structure:

```bash
├── jenkins-configs
│   ├── jobs
│   │   └── TOM
│   └──      └── config.xml
├── mishosts
├── playbookG.yaml
├── requirements.yml
├── vagrantfile	
├── example.crt
└── example.key	

```
This process deploys a forked version of timeoff management app hosted in: https://github.com/timeoff-management/timeoff-management-application.

In the forked repo https://github.com/nat55555/timeoff-management-application the following files have been added/modified: docker-compose.yml, Dockerfile and Jenkinsfile


## Instructions

1. Install dependencies
    
    `ansible-galaxy install -r requirements.yml`
    
2. Run

    `vagrant up`
    
    Wait until the comand finishes it's execution, this may take a couple minutes.
    
3. Check connectivity to applications

   Jenkins: Open http://192.168.86.86:9999/ in your browser (default credentials: admin/admin).  
   Nexus: Open http://192.168.86.86:8081/ in your browser (default credentials: admin/changeme).

4. Check CI/CD setup

   Login in jenkins with the default credentials (admin/admin)  
   Check the existence of the job TOM (this is a pre-defined job that can be used to deploy the app)  
   Click the "configure" icon and save (to reload Sandbox)  
   Click build (the first execution will fail due to lack of parameters)
   Click "Build with parameters" and select the branch from which you want to deploy the code

5. Check App

   After the pipeline completes it's execution, you can access the TimeOff.Management application by opening http://192.168.86.86:3333/ in your browser.


## Loose Ends

- The initial approach considered using GitLab as a local git repository, however the GitLab role did not work as planned (issues with Ansible resources and not being able to skip the initial change password GUI).
- Without a local GitLab it was not possible to activate the web-hook (public ip cannot reach private ip).
- Then, the option left was a GitHub SCM poll and the implementation was done that way (but more time would be needed for the right testing).
- Initial Artifactory approach did not work due to a known issue in Centos 7 for the role tested.
- Nexus default image does not run over SSL by default and the docker push command in recent versions does not support pushing to unsecure repos.
- More time would be needed to deploy an SSL version of a repository manager (for instance Apache reverse proxy for Nexus) -Stage to deploy to Nexus server is left commented on the Jenkins file to be tested with the SSL Nexus-.

## To-do list

### SSL
- Run Jenkins Over SSL to imporve security
- Add a nginx reverse-proxy to run nginx with ssl in order to avoid issue pushing docker to insecure repos

### USERS
- Use NON-Admin Accounts in the different tools
- disable anonymous login in jenkins

### TOOLS
- Set up static code analyzer
- Set up notifications to e-mail or Slack channel -Slack example was left comented in the jenkinsfile-

### PROCESS
- Define and implement a strategy for monitoring the application in production

