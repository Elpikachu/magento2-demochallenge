# Magento 2 Community Edition on Platform.sh

This template permits to build Magento 2 CE on PSH and showcase the build, deploy and management of the application.
The application is configured to use the following services & runtimes:
* MariaDB
* Redis
* Opensearch
* RabbitMQ
* PHP 8.1

With the help of some additional packages, like the ece-tools, the deploy becomes easier and faster.

## Projects
- Platform.sh: https://console.platform.sh/solutions/7qkgq43qy3qcu 
- Upsun: https://console.upsun.com/solutions/zgs2f2ea3vmli 


## Customizations needed to run
These customizations are needed in case you need to run the demo outside of the demos repo.

### Magento repo authentication
The access to the Magento repo needs you to authenticate before pulling the code.
You can use the CSA account on Magento to get the keys (All creds are stored in Vault).
```
platform variable:create -p <your Platform.sh projectID> --level project --name env:COMPOSER_AUTH --json true --visible-runtime false --sensitive true --visible-build true  --value '{"http-basic":{"repo.magento.com":{"username":"[public key]","password":"[private key]"}}}'
```

## How to run
### Admin access
An admin user is created if none exist through the `adminuser_setup.sh` script.

## Disabling TFA
In order to have an easier back office access, TFA is disabled as part of the deploy hook using the following command:
```
bin/magento config:set twofactorauth/general/enable 0
```

### Site performance
In order to have a quick deploy time for showcases, we have put the SCD on demand, which means that the first access will be slow. Please take a moment to do some cache warming before the demo

## Differences with Vanilla Magento
We have added some patches packages in order to have a clean install.
We also added the ECE tools, which is a set of tools that help in building and deploying Magento 2 on Platform.sh.
The ECE tools configuration is partly managed by the `.magento.env.yaml` file in the Git repo. The build and deploy scenarios can be found in the associated vendor directory.

## Contribution
- Maintainer: @julien.khamis