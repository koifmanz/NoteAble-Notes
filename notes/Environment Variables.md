---
tags: [Notebooks/DevOps]
title: Environment Variables
created: '2020-10-28T12:28:28.484Z'
modified: '2020-10-28T12:34:07.755Z'
---

# Environment Variables

### Linux / mac

Assume you store the user-specific secrets, such as username, password, or private key, into a simple file. It might not be a safe approach because all the sensitive information may become public if you put that information on Github/any other Version Control System. User-specific secrets, visible publicly, are never a good thing.

Here comes the role of Environment variables in this scenario. Environment variables are pretty much like standard variables, in that they have a name and hold value. The environment variables only belong to your local system and won't be visible when you push your code to a different environment like Github.

In the terminal enter the following code (also for password, host, etc):
```bash
export POSTGRES_USERNAME = yourUsername
export POSTGRES_PASSWORD = yourpassword
```

in your code's config file refer to variables by using (at least for node)
```config
"username": process.env.POSTGRES_USERNAME
```

One can config the terminal itself by using te follwoing and enter the variables. 
```bash
code ~/.profile
```

and if one wish to instruct your Node to execute the .profile file anytime, you can run the following command:
```bash
source ~/.profile
```
