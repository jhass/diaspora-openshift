# diaspora* for OpenShift

## This is currently broken until OpenShift adds support for Rails 4.2!
## See https://bugzilla.redhat.com/show_bug.cgi?id=1184179

This repository contains modifications to diaspora* for easy deployment.

## Installation

- Create an account on [OpenShift](https://openshift.redhat.com/app/)
- Install the CLI tool, `gem install rhc`, don't forget to run `rhc setup`.
- If you have none yet generate a SSH keypar: `ssh-keygen`.
- Create the application:

  ```bash
  rhc app create diaspora ruby-2.0 postgresql-9.2 'http://cartreflect-claytondev.rhcloud.com/reflect?github=smarterclayton/openshift-redis-cart'

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

**Note**: Unfortunately due to changes in diaspora* 0.5, it got incompatible with
the MySQL installed on OpenShift, upgrading diaspora* 0.4 installed from this
repository to diaspora* 0.5 is not possible! Instead make a backup of your MySQL
database, delete your app and create a new one with the same name as described above,
then import the backup of your MySQL database into PostgreSQL.

- Go into your local clone.
- Run `git pull upstream master`.
- Run `git push origin master`.
- It's time for another coffee.
