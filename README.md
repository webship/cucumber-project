# Cucumber Project

Composer project template for [Cucumber](https://www.drupal.org/project/cucumber),
the Automated Functional Acceptance Testing Management system built on Drupal.

It gives you a Drupal codebase with the `web/` docroot, the contrib installer
paths and the Cucumber distribution already required — nothing else. Use it as
the starting point for a new Cucumber site.

## Create a site with DDEV

[DDEV](https://ddev.readthedocs.io/en/stable/users/install/ddev-installation/)
is the documented way to run Cucumber. Composer, PHP, Drush and the database
all run inside DDEV, so nothing is needed on your machine but DDEV itself.

```shell
mkdir my-site && cd my-site
ddev config --project-type=drupal --docroot=web
ddev start
ddev composer create-project drupal/cucumber_project:~12.0
ddev restart
ddev drush site:install cucumber --account-name=webmaster --account-pass=<password> -y
ddev launch
```

`ddev restart` is there because the template ships its own
`.ddev/config.yaml` (PHP 8.3, Node.js 22, MariaDB 10.11), which lands in the
project during `ddev composer create-project` and replaces the one
`ddev config` wrote. The project name is not in that file: DDEV takes it from
the directory, so the site is at `https://<directory>.ddev.site`.

The installer asks which user roles, recipes and demo to add. To answer those
questions in a browser instead, skip the `site:install` line and run
`ddev launch` right away.

Drush lives at `bin/drush`, not `vendor/bin/drush`: the template sets the
Composer `bin-dir` to `bin/`, following the Cucumber profile. `ddev drush`
finds it either way.

## Without DDEV

The same template works with a Composer, PHP and database stack of your own:

```shell
composer create-project drupal/cucumber_project:~12.0 my-site --no-interaction
cd my-site
bin/drush site:install cucumber --account-name=webmaster --account-pass=<password> -y
```

## Requirements

* DDEV — or PHP 8.3 or newer, Composer 2 and a MySQL/MariaDB database.
* Drupal core `^11.4 || ^12`. Drupal 11.4 on PHP 8.3 is the tested default.

## Stability

Like every `drupal/*_project` template, this one sets `"minimum-stability": "dev"`
with `"prefer-stable": true`. Everything that has a stable release is installed
stable; the handful of Cucumber dependencies that do not yet have one
(Display Builder, Media Directories) are resolved to their newest pre-release.

`drupal/media_directories`, `drupal/media_directories_ui` and
`drupal/media_directories_editor` carry an explicit `^3.0@rc` constraint in the
root `require`. Their newest *stable* release is a Drupal 9-only 2.0.x, so
without the flag `prefer-stable` picks a version that Drupal 11 refuses to
install.

## Links

* Project page: https://www.drupal.org/project/cucumber
* Issue queue: https://www.drupal.org/project/issues/cucumber
* Source: https://git.drupalcode.org/project/cucumber_project
