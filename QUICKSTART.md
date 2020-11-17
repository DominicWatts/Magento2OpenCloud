# Quickstart Guide

## 1 Fetch from git

git clone git@github.com:DominicWatts/Magento2CloudDocker.git ./

## 2 Add the following entry to OS hosts file

    127.0.0.1 magento2.docker
       
## 3 Download

Inside `./`

### 3.1 Hypernode

    wget -qO- https://magento.mirror.hypernode.com/releases/magento2-latest.tar.gz | tar xfz -

Or

    wget -qO- https://magento.mirror.hypernode.com/releases/magento-2.3.4.tar.gz | tar xfz -

### 3.2 Direct Download
 
Download magento from https://magento.com/tech-resources/download
 
## 4 Start Containers

Inside `./`

Create bash history file

    touch .docker/bash/.bash_history

Copy newrelic.sample.ini config file to newrelic.ini and add new tokens if required

    cp .docker/newrelic/newrelic.sample.ini .docker/newrelic/newrelic.ini

Start Docker

    docker compose up -d

Or specific config file

    docker-compose -f docker-compose.no.varnish.yml up -d
    
Note: wait for MySQL to initialise if running for first time
 
## 5 Install

### 5.1 CLI

    docker-compose run --rm cli magento-command setup:install --admin-firstname Admin --admin-lastname User --admin-email dominic@xigen.co.uk --admin-user admin --admin-password test123 --base-url http://magento2.docker/ --base-url-secure https://magento2.docker/ --backend-frontname xpanel --db-host db --db-name magento2 --db-user magento2 --db-password magento2 --language en_GB --currency GBP --timezone UTC --use-rewrites 1 --session-save files --use-secure 1 --use-secure-admin 1
    
### 5.2 Elasticsearch

New for magento 2.4 - above command plus two additional arguments

    --elasticsearch-host elasticsearch --elasticsearch-port 9200

### 5.3 Web Setup Wizard (REDIRECT LOOP)

Official nxginx image is for Cloud so web interface gets into a redirect loop

http://magento2.docker/setup/

  - **db host:** db
  - **db name:** magento2
  - **db user:** magento2
  - **db password:** magento2
  
## 6 Tweak

PHP settings can be adjusted via

    `./php.ini`
