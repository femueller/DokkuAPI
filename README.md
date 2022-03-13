# Dokku API
Dokku API - API to interface with a Dokku installation

This API is built with FastAPI and you can access the docs after installation at [dokku-api-domain]/docs. You can also use the FastAPI docs to test and trial the api methods.


# Introduction
This api allows access with a Dokku installation with an HTTP REST API. This enables more possibilities to remote management of a Dokku server and also for automate application deployment. 

The goal is to provide a standard way of accessing Dokku installations with a remote API, something that Dokku is missing.


# Features
Current supported features:
- Apps (list, create, delete)
- Plugins (list, check if plugin is installed, install, uninstall), currently only supports Postgres, MySQL and LetsEncrypt plugins
- Databases (list, check database exists, create, delete, list linked apps, link, unlink)
- Domains (set, remove, set LetsEncrypt root mail, enable LetsEncrypt for app, enable auto renewal)

More features are planned to be added soon. The current features allows to deploy an application, set a datastore (database), set domain and enable HTTPS certificates.

# Security
No security is currently implemented in the API. After deployment it is available on the deployment URL or IP:PORT address with ACL.


# Pre-requisites
You need access to a Dokku server to install Dokku API as a application. If you don't have a Dokku server, please create a server first. I recommend Digital Ocean since you can get an automatic Dokku installation.

On the Dokku server the following needs to be configured:
```
# Create a Dokku application
$ dokku apps:create dokku-api
```

The Dokku API depends on a couple of ENV variables for specific settings, so the following ENV values must be configured:
```

dokku config:set dokku-api
API_NAME="Dokku API"
API_VERSION_NUMBER="0.1"
SSH_HOSTNAME="10.20.0.25"
SSH_PORT="22"
SSH_KEY_PATH="ssh_private_key"
SSH_KEY_PASSPHRASE="labolg3189981bispo"

```


The Dokku API also depends on SSH access to the Dokku server to run the commands, which means that SSH keys must be configured and mounted on the Dokku API application.
```

sudo mkdir /dokku-api

sudo nano /dokku-api/id_rsa

dokku storage:mount dokku-api /dokku-api/:/dokku-api/

dokku config:set SSH_KEY_PATH="/dokku-api/id_rsa"

```

# Installation
```
# Clone project
$ git clone https://github.com/nunombispo/DokkuAPI.git

# Add your Dokku server as a remote
$ git remote add dokku dokku@[domain]:dokku-api

# Push repository to Dokku
$ git push dokku
```


You can check additional options on configuring a domain and HTTPS on Dokku Docs: https://dokku.com/docs/deployment/application-deployment/

# Contributing
All contribuitions are welcome
