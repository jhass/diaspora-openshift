# diaspora* for OpenShift

diaspora* is a privacy-aware, personally-controlled, do-it-all open source social network. Check out our [project site](https://diasporafoundation.org) and the [main repository](https://github.com/diaspora/diaspora).

[OpenShift](https://openshift.redhat.com/app/) is a hosting platform by RedHat.

This repository contains modifications to diaspora* for easy deployment.

## Installtion

- Create an account on [OpenShift](https://openshift.redhat.com/app/)
- Install the CLI tool, `gem install rhc`, don't forget to run `rhc setup`.
- If you have none yet generate a SSH keypar: `ssh-keygen`.
- Create the application:
  
  ```bash
  rhc app create diaspora \
     ruby-2.0 mysql-5.5 \
     'http://cartreflect-claytondev.rhcloud.com/reflect?github=smarterclayton/openshift-redis-cart'

  ```
  
- If it asks you to upload your SSH key, answer yes.
- Run the following commands:
  
  ```bash
  cd diaspora
  git remote add upstream git://github.com/jhass/diaspora-openshift.git
  git fetch upstream
  git reset --hard upstream/master
  git push -f origin master
  ```
  
- Grab a coffee.

## Configuration

Configuration is done via environment variables. To change something
from the default set them via `rhc env set`, see `rhc help env`. To see what's available,
read `config/diaspora.yml.example`.

### Adding yourself as an admin

After you created an account on your new diaspora* pod, you can make
yourself an admin with: `rhc ssh diaspora -- '/bin/bash -c "cd $OPENSHIFT_REPO_DIR; source .openshift/diaspora_configuration; bundle exec rails runner \"Role.add_admin(User.where(username: \\\"your_username\\\").first.person)\""'`.


## Updating

- Go into your local clone.
- Run `git pull upstream master`.
- Run `git push origin master`.
- It's time for another coffee.
