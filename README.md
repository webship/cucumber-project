# Cucumber Project

Composer project template for [Cucumber](https://www.drupal.org/project/cucumber),
the Automated Functional Acceptance Testing Management system built on Drupal.

It gives you a Drupal codebase with the `web/` docroot, the contrib installer
paths, the Cucumber distribution and its site template,
[Cucumber Starter](https://www.drupal.org/project/cucumber_starter), already
required, and nothing else. Use it as the starting point for a new Cucumber
site.

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
ddev drush site:install cucumber --account-name=webmaster --account-pass=<password> --site-name="<site name>" -y
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

The site asks everybody to sign in: a visitor who is not signed in is sent to
`/user/login`, and lands on a dashboard after signing in.

### With the site template

The template also places the Cucumber Starter site template in
`recipes/cucumber_starter`. To install the site from it, the way Drupal CMS
installs a site template, replace the `site:install` line with:

```shell
ddev drush site:install ../recipes/cucumber_starter --account-name=webmaster --account-pass=<password> --site-name="<site name>" -y
```

The site template brings the Admin role and the three recipes. The other
roles are turned on at
`/admin/config/development/cucumber-user-roles/settings`.

Drush lives at `bin/drush`, not `vendor/bin/drush`: the template sets the
Composer `bin-dir` to `bin/`, following the Cucumber profile. `ddev drush`
finds it either way.

## Drupal 12 (beta)

The template installs the latest Drupal 11 by default. It also allows Drupal 12,
which needs PHP 8.5. To try it, set `php_version: "8.5"` in `.ddev/config.yaml`
(a DDEV release with PHP 8.5 is needed), then:

```shell
ddev restart
ddev composer require drupal/core:^12 drupal/core-composer-scaffold:^12 drupal/search:^1 -W
```

Search left Drupal core in Drupal 12; Cucumber uses it, so the contrib
`drupal/search` module comes with the upgrade.

Contributed modules that don't declare Drupal 12 support yet are allowed by the
`mglaman/composer-drupal-lenient` plugin (`extra.drupal-lenient.allowed-list`).
Some of them still fail on Drupal 12.

## Requirements

* DDEV.
* Drupal core `^11.4`, or `^12` with PHP 8.5. Drupal 11.4 on PHP 8.3 is the tested default.

## Stability

Like every `drupal/*_project` template, this one sets `"minimum-stability": "dev"`
with `"prefer-stable": true`. Everything that has a stable release is installed
stable; the handful of Cucumber dependencies that do not yet have one
(Display Builder) are resolved to their newest pre-release.

`drupal/media_directories`, `drupal/media_directories_ui` and
`drupal/media_directories_editor` carry an explicit `^3.0@rc` constraint in the
root `require`, which keeps Composer away from their 2.0.x releases: those are
for Drupal 9 only, and Drupal 11 refuses to install them.

## Where the packages come from

Everything Cucumber is made of comes from drupal.org: the modules and the
theme from `packages.drupal.org`, and the `drupal/cucumber_starter` site
template from its drupal.org repository. The distribution itself is required
as `webship/cucumber`, the name its `composer.json` carries:
`packages.drupal.org` does not serve installation profiles, so there is no
`drupal/cucumber` package to require.

## Links

* Project page: https://www.drupal.org/project/cucumber
* Issue queue: https://www.drupal.org/project/issues/cucumber
* Source: https://git.drupalcode.org/project/cucumber_project
