[![Build Status](https://travis-ci.org/shopwareLabs/shopware-docker.svg?branch=master)](https://travis-ci.org/shopwareLabs/shopware-docker)

Docker Shopware Box
====================

## Installation

Docker (min. Version 1.12) have to be installed on your local machine:

 - [Docker](https://docs.docker.com/engine/installation/linux/)

## Usage

Clone the repository to your local machine.

    $ git clone https://github.com/shopwareLabs/shopware-docker
    $ cd shopware-docker

Boot up your docker containers with psh.phar:

    $ ./psh.phar docker:start

The first boot may take a while, so feel free to get a cup of coffee.

Your machine will be available at [http://localhost:8083/](http://localhost:8083/)
All required tools like the LAMP stack are already installed.

- MySQL user: `app`, password: `app`

To SSH into the created Container:

    $ ./psh.phar docker:ssh

## Installing Shopware

SSH first into your VM:

    $ ./psh.phar docker:ssh
    
Call the init script:

    $ ./psh.phar init
    
This will download the latest release version of shopware and install it into /var/www/shopware/shopware

If you want an older shopware version just add --sw-version to the init script:

    $ ./psh.phar init --sw-version=5.7.17

If an error occurs during unzip and you are asked whether data should be overwritten, then the release is defective. Just choose another release.

Add config to disable cache and force compile of template on every refresh:

    // config.php
    array(
        ...
        'template' => [
            'forceCompile' => true,
        ]
        ...
    )

#### For plugin development

> This does not work! I put fucking 6 hours into it trying to fix the dev environment.... but functions are called which don't exist since > 5.2. No alternative functions exist. From one error message to the next!
>
> Just use `init`... and that's it. (See above)
> 
> Dome

For plugin development there is a script `init-vcs` to initialize and install shopware through github.  

    $ ./psh.phar init-vcs --sw-branch=5.7

The plugin(s) you want to start development should be located in `./plugins` (Only new plugin system is supported). They can be installed and linked into the Shopware checkout by executing

    $ ./psh.phar init-plugins
    

This can be used together with our [`plugin-dev-tools`](https://github.com/shopwareLabs/plugin-dev-tools) as the `local` environment.

#### Access

Configure your online store in a web browser with the credentials demo/demo:

- Backend: [http://localhost:8083/backend/](http://localhost:8083/backend/)

You can then access your storefront at:

- Front-end: [http://localhost:8083/](http://localhost:8083/)

## Troubleshooting 

If the elasticsearch or redis container didn't start make sure that the directory dev-ops/docker/_volumes/app-esdata|app-redisdata has chmod 777.
