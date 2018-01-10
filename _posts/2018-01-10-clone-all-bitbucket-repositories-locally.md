---
type: post
title: "Clone all your Bitbucket repositories locally"
meta-description: "Simple preparations in case of a service failure."
---

Following [latest Bitbucket incident](https://status.bitbucket.org/incidents/z029156p1svh), you may ask what could happen if the service would crash? You'll loose all your repos? How could you prevent this?

Last year GitLab had a [serious incident with one of their databases](https://about.gitlab.com/2017/02/01/gitlab-dot-com-database-incident/) and they lost six hours of database data (issues, merge requests, users, comments, snippets, etc.) for GitLab.com.

No matter what you are using, if the service goes down, what can you do to save your data and how can you protect yourself in case of a service failure?

Let's start with the simplest measurement you can take. We will clone all your Bitbucket repos locally.

Using Bitbucket API:
 * [/2.0/repositories/{username}](https://developer.atlassian.com/bitbucket/api/2/reference/resource/repositories/%7Busername%7D)

You can get a list of repos under your account. Having this list you can iterate `git clone` over project names.

For this we will use the `bitbucket-backup` python script, made by [samkuehn](https://github.com/samkuehn/bitbucket-backup).

Install Python, if you don't have it already in your system. [Download binaries here](https://www.python.org/downloads/).

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
python bitbucket-backup -u bitbucket_user -l repos --http
```

Enter password and wait... your repositories will be downloaded and cloned locally in `repos` folder.

```bash
2018-01-10 09:18:38.949947 - Backing up [repo1]...
2018-01-10 09:18:41.641931 - Backing up [repo2]...
2018-01-10 09:18:43.937138 - Finished!
```

Running the same command again will update the existing repositories.

Even more info:
```bash
usage: bitbucket-backup [-h] [-u USERNAME] [-p PASSWORD] [-k OAUTH_KEY]
                        [-s OAUTH_SECRET] [-t TEAM] [-l LOCATION] [-v] [-q]
                        [-c] [-a ATTEMPTS] [--mirror] [--with-wiki] [--http]
                        [--skip-password] [--prune]
                        [--ignore-repo-list IGNORE_REPO_LIST [IGNORE_REPO_LIST ...]]

Usage: %prog [options]

optional arguments:
  -h, --help            show this help message and exit
  -u USERNAME, --username USERNAME
                        Bitbucket username
  -p PASSWORD, --password PASSWORD
                        Bitbucket password
  -k OAUTH_KEY, --oauth-key OAUTH_KEY
                        Bitbucket oauth key
  -s OAUTH_SECRET, --oauth-secret OAUTH_SECRET
                        Bitbucket oauth secret
  -t TEAM, --team TEAM  Bitbucket team
  -l LOCATION, --location LOCATION
                        Local backup location
  -v, --verbose         Verbose output of all cloning commands
  -q, --quiet           No output to stdout
  -c, --compress        Creates a compressed file with all cloned repositories
                        (cleans up location directory)
  -a ATTEMPTS, --attempts ATTEMPTS
                        max. number of attempts to backup repository
  --mirror              Clone just bare repositories with git clone --mirror
                        (git only)
  --with-wiki           Includes wiki
  --http                Fetch via https instead of SSH
  --skip-password       Ignores password prompting if no password is provided
                        (for public repositories)
  --prune               Prune repo on remote update
  --ignore-repo-list IGNORE_REPO_LIST [IGNORE_REPO_LIST ...]
                        specify list of repo slug names to skip

```

The following script is tested and working on Windows with:
 * Git for Windows 12.15.1
 * Python 3.6.4
