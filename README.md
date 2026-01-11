# Secure Secrets with Secrets Manager

This project demonstrates how to protect your application and integrated resources from unauthorized access by securely storing access credentials in  AWS Secrets Manager. 

### Tools and concepts

Services I used were;

- AWS Secrets Manager

- AWS Identity and Access Management (IAM)

- Github's Secret Scanning feature 

Key concepts I learnt include:
1. Creating and managing secrets using Secret Manager
2. Using Github's Secret Scanning feature to scan for hardcoded credentials.

### Project reflection

This project took me approximately 1hr. It was most rewarding to use AWS Secrets Manager to ensure that my code does not expose any secret credentials.

I chose to do this project today because I wanted to learn how to manage security credentials to prevent accidental exposure.

---

## Hardcoding credentials

In this project, a sample web app is exposing access credentials (access key ID and secret key) on code that is publicly available on Github. It is unsafe to harcode credentials because once an attacker gets access to this code,they will gain access to other resources, steal information and probably defaceor sabotage your application. These credentials are not only AWS credentials, it could be API keys for other services or, database passwords.

I've set up the initial configuration with the access key ID and secret access key. These credentials are just examples because it would be such a huge risk to expose my actual AWS credentials 😅

![Image](http://learn.nextwork.org/calm_chartreuse_playful_saci_perere/uploads/aws-security-secretsmanager_j2k3l4m5)

---

## Using my own AWS credentials

As an extension for this project, I also decided to run the application practically using my AWS credentials. Very risky. But I wanted to demonstrate just how much risk it is to expose credentials. To set up my virtual environment, I installed boto3, the AWS SDK for Python to enable me access S3 buckets. 

When I first ran the app, I ran into an error "InvalidAccessKeyID". This was because I used dummy AWS credentialsd. To see the application in action, I'll add my actual AWS credentials.

To resolve the 'InvalidAccessKeyId' error, I updated the config.py  file to add actual access credentials.

---

## Pushing Insecure Code to GitHub

Once I updated the web app code with credentials, I forked the repository because I want to have my own version of the code and edit it online. A fork is different from a clone because a clone enables you to make a copy of the code and edit it offline on your computer.

To connect my local repository to the forked repository, added a remote called "origin". Then I used git add and git commit to c commit the changes I had made on the config file (add my credentials) . Finally, git push uploads the code onto the forked repository.

GitHub blocked my push because the code contained secret keys that shouldn't be exposed. This is a good security feature because it prevents you from accidentally exposing sensitive information.

![Image](http://learn.nextwork.org/calm_chartreuse_playful_saci_perere/uploads/aws-security-secretsmanager_o2p3q4r5)

---

## Secrets Manager

Secrets Manager is an AWS service used to store and manage secrets like API keys and database credentials I'm using it to store my access credentials ( access key ID and secret key) Other common use cases include rotating secrets and tracking access to secrets for security audit.

Secret rotation is a key feature of secrets manager because it automatically changes your secrets on a regular schedule. This reduces the impact that would result from use of compromised credentials in cyber attacks. It's useful in situations where you are using high-risk credentials like database passwords, API keys and service account credentials.

Secrets Manager provides sample code to allow you retrieve the secrets in your code. The sample code comes in various languages, like Java, Javascript, Python, Go among others. This is helpful because it allows you to easily integrate it into your application, regardless of the programming language you used.

![Image](http://learn.nextwork.org/calm_chartreuse_playful_saci_perere/uploads/aws-security-secretsmanager_h2i3j4k5)

---

## Updating the web app code

I updated the config.py file to retrieve credentials from the Secrets Manger. The get_secret() function will retrieve the secret named "s3bucketlistsecret" from the Secrets Manager.

I also added code to config.py to extract the Access Key ID, the Secret Key, and the region within which the Secrets Manager is Located. This will help retrieve the actual credentials that will be used by the app to list S3 buckets.

![Image](http://learn.nextwork.org/calm_chartreuse_playful_saci_perere/uploads/aws-security-secretsmanager_v0w1x2y3)

---

## Rebasing the repository

Git rebasing is the process of re-writing the commit history. I used it to remove the commit that contained hardcoded credentials. This was necessary because git still wouldn't push my changed code since it still had the commit that contained the hardcoded credentials.


![Image](http://learn.nextwork.org/calm_chartreuse_playful_saci_perere/uploads/aws-security-secretsmanager_t5u6v7w8)

A merge conflict occurred during rebasing because I changed the same line of code (the lines containing credentials and region values) in different commits. I resolved the merge conflict by removing the code that contained the hardcoded credentials and keeping the secure version.

Once the merge conflict was resolved, I verified that the config.py file does not show hardcoded credentials but instead, uses the get_secret() function to retrieve the credentials from Secrets Manager.

![Image](http://learn.nextwork.org/calm_chartreuse_playful_saci_perere/uploads/aws-security-secretsmanager_r7s8t9u0)
---

---
