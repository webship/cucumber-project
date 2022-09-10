[![Build Status](https://travis-ci.org/webship/cucumber.svg?branch=9.0.0-alpha2)](https://travis-ci.com/github/webship/cucumber/builds/205034599) Cucumber 9.0.0-alpha2

# Cucumber Project

Cucumber Automated Functional Acceptance Testing Management system

The app.webship.co console dashboard system was built on top of Drupal, as it has many options, tools, frameworks, and configuration management, which are needed in building solutions.

Helps in speeding up the work of having Functional Automated Acceptance Testing for products to ship websites in a swift way.

[![Cucumber](https://www.drupal.org/files/project-images/drupal-cucumber.png)](https://www.drupal.org/project/cucumber)

### We LOVE to help with:
* Setup of Automated Functional Testing configurations for projects.
* Writing Cucumber descriptions, Gherkin scripts for web apps.
* Development of Webship-js using Nightwatch.js, Cucumber-js with custom and advanced general step definitions.
* Setup Selenium robot servers, and Web-drivers to work on a local development, CircleCI, Github Actions, Gitlab-CI, Travis-CI, Bitbucket Pipelines and private CI/CD servers.

## Usage

First you need to [install composer](https://getcomposer.org/doc/00-intro.md#installation-linux-unix-osx).

> Note: The instructions below refer to the [global composer installation](https://getcomposer.org/doc/00-intro.md#globally).
You might need to replace `composer` with `php composer.phar` (or similar) 
for your setup.

To install the most recent stable release of Cucumber 9.0.x run this command:
```
composer create-project webship/cucumber-project:^9.0.0-alpha2 WEBSITE_NAME --no-dev --no-interaction
```

To install the dev version of Cucumber 9.0.x run this command:
```
composer create-project webship/cucumber-project:9.0.x-dev WEBSITE_NAME --stability dev --no-interaction
```