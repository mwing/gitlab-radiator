# The missing GitLab build radiator view

## Introduction

```gitlab-radiator``` is a small Node.js application for serving an [Jenkins Radiator View](https://wiki.jenkins-ci.org/display/JENKINS/Radiator+View+Plugin) inspired web view of your team's builds fetched from an GitLab CI installation running locally or remotely.

<img src="https://raw.github.com/heikkipora/gitlab-radiator/master/screenshot.png" width="50%">

[![npm version](https://badge.fury.io/js/gitlab-radiator.svg)](https://badge.fury.io/js/gitlab-radiator)
[![build status](https://travis-ci.org/heikkipora/gitlab-radiator.svg?branch=master)](https://travis-ci.org/heikkipora/gitlab-radiator)

## Pre-requisites

- Node.js v5.0.0 or newer
- A modern web browser
- An account in https://gitlab.com or an onsite installation of the GitLab software package.

## Installation

    npm install -g gitlab-radiator

## Usage

Create a configuration file (see [Configuration](#configuration) below) and run:

    gitlab-radiator

And if you have an onsite GitLab with HTTPS and self-signed certificates:

    NODE_TLS_REJECT_UNAUTHORIZED=0 gitlab-radiator

You might prefer providing the CA file location in configuration instead of totally disabling TLS certificate checking.

Then navigate with a browser to http://localhost:3000 - or whatever port you did configure.

## Configuration

```gitlab-radiator``` looks for its mandatory configuration file at ```~/.gitlab-radiator.yml``` by default.
It can be overridden by defining the ```GITLAB_RADIATOR_CONFIG``` environment variable.

Mandatory configuration properties:

- ```gitlab / url``` - Root URL of your GitLab installation - or that of GitLab SaaS CI
- ```gitlab / access-token``` - A GitLab access token for allowing access to the GitLab API. One can be generated with GitLab's UI under Profile Settins / Personal Access Tokens.

Example yaml syntax:

```
gitlab:
  access-token: 12invalidtoken12
  url: https://gitlab.com
```

Optional configuration properties:

- ```projects / include``` - Regular expression for inclusion of projects. Default is to include all projects.
- ```projects / exclude``` - Regular expression for exclusion of projects. Default is to exclude no projects.
- ```intervals / projects``` - Number of seconds between project list updates. Default value is 120 seconds.
- ```intervals / builds``` -  Number of seconds between build state updates. Default value is 10 seconds.
- ```port``` - HTTP port to listen on. Default value is 3000.
- ```zoom``` - View zoom factor (to make your projects fit a display nicely). Default value is 1.0
- ```caFile``` - CA file location to be passed to the request library when accessing your gitlab instance

Example yaml syntax:

```
projects:
  include: .*/my-awesome-project-.*

intervals:
  projects: 600
  builds: 30

port: 8000
zoom: 0.85
```

## Contributing

Pull requests are welcome. Kindly check that your code passes ESLint checks by running ```npm test``` first.

## Contributors
 - Antti Oittinen ([codegeneralist](https://github.com/codegeneralist))
