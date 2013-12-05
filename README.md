# diaspora* for OpenShift

diaspora* is a privacy-aware, personally-controlled, do-it-all open source social network. Check out our [project site](https://diasporafoundation.org) and the [main repository](https://github.com/diaspora/diaspora).

[OpenShift](https://openshift.redhat.com/app/) is a hosting platform by RedHat.

This repository contains modifications to diaspora* for easy deployment.

**NOTE:** The status of this is experimental, OpenShift lacks a sane mechanism for configuration management. Until that changes I won't further develop this and wouldn't recommend to actually run diaspora* on OpenShift.

## Installtion

- Create an account on [OpenShift](https://openshift.redhat.com/app/])
- Create a Ruby on Rails app.
- Change the source code to `git://github.com/MrZYX/diaspora-openshift.git` while doing that
- Go to the "Application Overview" page.
- Grab a coffee.
- Wait until the apps status  says "Started". This takes quite some time.

## Configuration
todo


## Updating

### First time setup

You can also use this to get hold of a local copy so that you can modify your diaspora*.

- If you have none yet generate a SSH keypar: `ssh-keygen`.
- Grab `~/.ssh/id_rsa.pub` and add it at the [My account](https://openshift.redhat.com/app/account) page under "Public Keys".
- Install [Git](http://git-scm.org) on your computer.
- Goto [your applications](https://openshift.redhat.com/app/console/applications) and there to your Diaspora application.
- Copy the "Git repository" URL
- Run `git clone your_git_repository_url`
- Go into it: `cd diaspora`.
- Run `git remote add upstream git://github.com/MrZYX/diaspora-openshift.git`

###  Every time you need to update

- Go into your local clone.
- Run `git pull upstream master`.
- Run `git push origin master`.
- It's time for another coffee.

## Issues

- There's a new secret token generated on every redeploy, so all users will get logged out on that.
- There's no straight forward way to configure your pod.
- There's no straight forward way to add yourself as an admin.
