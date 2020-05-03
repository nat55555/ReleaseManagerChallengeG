# ReleaseManagerChallengeG
Release Manager Challenge

## Pre requisites

- ansible

  For MacOS: `brew install ansible`

- vagrant

  For MacOS: `brew cask install vagrant`

- virtualbox

  For MacOS: `brew cask install virtualbox`

## About

This setup allows the CI/CD

## Instructions

1. Install depenencies
    
    ansible-galaxy install -r requirements.yml 
    
2. Run

    vagrant up
    
3. Check connectivity to applications

4. Check CI/CD setup

5. Monitor App 

## TODOS

### SSL
- Run Jenkins Over SSL to imporve security
- Add a nginx reverse-proxy to run nginx with ssl in order to avoid issue pushing docker to insecure repos

### USERS
- Use NON-Admin Accounts in the different tools
- disable anonymous login in jenkins

## TOOLS
- Setup static code Analyzer


## Author

Natalia Cardona
