---
title: Npm commands for npm noobs
date: 2020-07-05
tags: [terminal, webdev, frontend]
---

Since diving more deeply into frontend development, I had troubles adjusting with the node ecosystem, more specifically to npm commands. I just keep on forgetting what the npm commands do. So here are my short notes on them.

## Basics

{{<highlight bash>}}

$ npm --version              # check npm version
$ npm install -g npm@latest  # update npm

{{</highlight>}}

#### Notes:

- npm packages can be installed locally or globally. 
- global packages are installed with **-g** flag or **- -global** flag
- all installed packages get stored in **node_modules** folder

## Package installation

{{<highlight bash>}}

# initialize a project that will contain node dependencies
$ npm init                    

# search for packages
$ npm search package_name

# install express package
$ npm install express    

# save package as a developer dependency (e.g. testing frameworks)
$ npm install express --save-dev 

# install a specific version of express
$ npm install express@1.2.3   

# uninstall express package
$ npm uninstall express       

# check installed packages
$ npm list --depth=0          # do with -g for global packages

{{</highlight>}}

#### Notes:

- npm init generates **package.json** file. Subsequent operations may generate a **package-lock.json** file
    - package.json tracks installed packages
    - package-lock.json ensures same dependencies are used across all machines

A cloned git repo will not have dependencies installed. But a package.json will be present. To install the dependencies from package.json run
{{<highlight bash>}}
$ npm install   # make sure you are in project directory
{{</highlight>}}

## Updating packages

{{<highlight bash>}}

# check for outdated packages
$ npm outdated    

# ~/.npm directory will get cluttered with old packages over time
# so clean it occasionally with
$ npm cache clean --force

# search for vulnerabilities in installed packages
$ npm audit

# updates packages to remove known vulnerabilities
$ npm audit fix

{{</highlight>}}

## npx

Whereas npm is a tool for managing packages, npx is a tool for executing packages.

{{<highlight bash>}}
# For example
npx http-server
{{</highlight>}}