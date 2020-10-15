---
title: "Gcloud command line auth"
date: 2020-06-05T13:56:58+01:00
draft: false
toc: false
images:
tags:
  - gloud
  - google cloud
  - terraform
  - command line
  - auth
---

This is how you can have multiple separate gcloud accounts(Client A, Client B, Home?) and switch between them on the command line.

## gcloud tools configurations
gcloud tools has this idea of configurations. These can contain multiple accounts which to me at least was confusing at first. 

### Add a configuration
If you're doing this for the first time then you need to set up your default configuration. Then every time you need to add a new configuration
```
gcloud init
```

### View configurations (created via gcloud init)
```
gcloud config configurations list
```

### Switch between configurations
```
gcloud config configurations activate $CONFIG
```


### Show or list a configurations settings
I found this command confusing. It lists the settings of your current configuration.
```
gcloud config list
```
To list the settings of a particular configuration:
```
gcloud config list --configuration $CONFIGURATION_NAME
```

### List and Switch between accounts within the same configuration
```
gcloud auth list
gcloud config set account
```


## Authenticate a 3rd party app like Terraform
The command for this is:
```
gcloud auth application-default login
```

