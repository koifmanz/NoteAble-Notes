---
tags: [Notebooks/AWS]
title: IAM
created: '2020-10-27T08:00:01.489Z'
modified: '2020-10-27T08:07:49.199Z'
---

# IAM

* IAM user role: an IAM role can give a user a set of permissions to access one or more services.
* IAM service role: an IAM role gives a service a set of permissions to access one or more services.
* It’s beneficial to create a role that contains a policy group (a set of permissions), rather than to assign individual permissions to a specific user. Imagine if a user leaves the company and a new hire takes their place. Instead of re-assigning all the permissions needed for their job, we can assign the existing IAM role to that new employee.

### CLI Configure

Use in cmd

```cmd
aws configure
```
 
his creates two new files on your local computer to save credentials and configurations.

Each of these files can contain settings for multiple "profiles" which are defined by using hard brackets containing the profile name preceding the variables (i.e. [profile1]). For example, if you're working on two or three systems, you will need installed credentials for each. You can modify these files in your text editor of choice to add and edit profiles and select the appropriate profile at runtime of your application. 

**~/.aws/credentials Example:**
```config
[default]
aws_access_key_id=########################
aws_secret_access_key=########################

[profile1]
aws_access_key_id=########################
aws_secret_access_key=########################

[profile2]
aws_access_key_id=########################
aws_secret_access_key=########################
```

**~/.aws/config Example:**
```config
[default]
region=us-east-1

[profile1]
region=us-west-2

[profile2]
region=us-east-2
```

These files are located in *:\Users\USERNAME* *.aws\config*


