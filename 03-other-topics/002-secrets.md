---
category: cloud-platform
expires: 2018-06-30
---
# Secrets overview

We identify secrets as one of three kinds:
- user secrets
- system secrets
- application secrets

## User Secrets

They are essentially any kind of secret that is owned by a specific user (eg. GitHub or AWS credentials). The user is responsible for securely managing these secrets, typically using a password manager and they should not be shared with other individuals or used in applications.

## System Secrets

They are secrets used in system components, usually configured by someone who manages, configures or supports the system. For example, when setting up a CI pipeline, the credentials it uses to fetch the source code and push the produced artifacts to a repository are considered system secrets.

These should not be tied to an individual user but machine users should be employed. The responsibility of managing these secrets securely lies with the owner of the system.

## Application Secrets

These are the secrets that the application requires at runtime. Some examples are: API keys for third-party services, keys that applications might use to communicate with each other, database credentials, cookie encryption keys and so on.

This kind of secrets falls under the shared responsibility model:

- the owners of the application are responsible for securely managing the secrets at rest (eg. using [git-crypt]({{ "/03-other-topics/001-git-crypt-setup" | relative_url }}) to encrypt them alongside the source code) and also for managing access to the secrets once they've been added to an environment,

- the Cloud Platform team, on the other hand, is responsible for ensuring the secrets remain secure inside the environment.
