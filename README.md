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
└── vagrantfile	

```

## Instructions

1. Install depenencies
    
    `ansible-galaxy install -r requirements.yml`
    
2. Run

    vagrant up
    
3. Check connectivity to applications

   Jenkins: Open http://192.168.86.86:9999/ in your browser.
   Nexus: Open http://192.168.86.86:8081/ in your browser.

4. Check CI/CD setup

   Login in jenkins with the default credentials (admin/admin).
   Check the existence of the job TOM (This is a pre-defined job that can be used to deploy the app)
   Click the "configure" icon and save (to reload Sandbox)
   Click build (the first execution will fail due to lack of parameters)

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


