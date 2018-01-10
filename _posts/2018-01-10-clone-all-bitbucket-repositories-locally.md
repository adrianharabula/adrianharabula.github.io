---
type: post
title: "Clone all your Bitbucket repositories locally"
meta-description: "Simple preparations in case of a service failure."
---

Following [latest Bitbucket incident](https://status.bitbucket.org/incidents/z029156p1svh), you may ask what could happen if the service would crash? You'll loose all your repos? How could you prevent this?

Last year GitLab had a [serious incident with one of their databases](https://about.gitlab.com/2017/02/01/gitlab-dot-com-database-incident/) and they lost six hours of database data (issues, merge requests, users, comments, snippets, etc.) for GitLab.com.

No matter what you are using, if the service goes down, what can you do to save your data and how can you protect yourself in case of a service failure?

Let's start with the simplest measurement you can take. We will clone all your Bitbucket repos to take snapshot of your code in current state.

Using Bitbucket API:
 * [/2.0/repositories/{username}](https://developer.atlassian.com/bitbucket/api/2/reference/resource/repositories/%7Busername%7D)

You can get a list of repos under your account. Having this list you can iterate `git clone` over project names.

We will use the `bitbucket-backup` python script, made by [samkuehn](https://github.com/samkuehn/bitbucket-backup).

Install python, if you don't have it already in your system. [Download binaries here](https://www.python.org/downloads/).

Clone / download `bitbucket-backup` python script:
```bash
git clone https://github.com/samkuehn/bitbucket-backup.git
cd bitbucket-backup
```
Run the script:
```bash
# use -u to specify username user to log in
# use -l to specify download location
# use -t to specify the team you want to download repositories from
# use --http to clone repositories with https instead of ssh
# see full list of parameters here https://github.com/samkuehn/bitbucket-backup/blob/master/README.md#quickstart
```

Sample command:
```bash
# download repositories owned by bitbucket_user to `repos` folder
# use https instead of ssh protocol
python bitbucket-backup -u bitbucket_user -l repos --https
```

Enter password and wait... your repositories will be downloaded and cloned locally.

```bash
2018-01-10 09:18:38.949947 - Backing up [repo1]...
2018-01-10 09:18:41.641931 - Backing up [repo2]...
2018-01-10 09:18:43.937138 - Finished!
```

Now in `repos` folder you have all your Bitbucket repos. Running the same command again will update the existing repositories.
