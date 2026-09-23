# Cucumber Project

Composer project template for [Cucumber](https://www.drupal.org/project/cucumber),
the Automated Functional Acceptance Testing Management system built on Drupal.

It gives you a Drupal codebase with the `web/` docroot, the contrib installer
paths and the Cucumber distribution already required — nothing else. Use it as
the starting point for a new Cucumber site.

## Usage

First you need to [install Composer](https://getcomposer.org/doc/00-intro.md#installation-linux-unix-osx).

Create the project:

```
composer create-project drupal/cucumber_project:~12.0 my-site --no-interaction
cd my-site
```

Then install the Cucumber distribution:

```
bin/drush site:install cucumber --account-name=webmaster --account-pass=<password> -y
```

Drush lives at `bin/drush`, not `vendor/bin/drush`: the template sets the
Composer `bin-dir` to `bin/`, following the Cucumber profile.

## Requirements

* PHP 8.3 or newer.
* Drupal core `^11.4 || ^12`.
* Composer 2.

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
