# dokku s3backup (alpha) 

AWS S3 backup plugin for dokku. Currently supports Postgres and CouchDB scheduled or manual backups to an AWS S3 bucket.


## requirements

- dokku 0.4.0+
- docker 1.8.x

## installation

```shell
# on 0.3.x
cd /var/lib/dokku/plugins
git clone https://github.com/urlsangel/dokku-s3backup.git s3backup
dokku plugins-install

# on 0.4.x
dokku plugin:install https://github.com/urlsangel/dokku-s3backup.git s3backup
```

## commands

```
postgres:create <name>            Create a s3backup service with environment variables
postgres:destroy <name>           Delete the service and stop its container 
postgres:list                     List all s3backup services
postgres:logs <name> [-t]         Print the most recent log(s) for this service
postgres:restart <name>           Graceful shutdown and restart of the s3backup service container
postgres:start <name>             Start a previously stopped s3backup service
postgres:stop <name>              Stop a running s3backup service
```

## usage

```shell
# create a s3backup service named fred
dokku s3backup:create fred

# set the backup vars using dokku config:set 
dokku config:set fred S3_REGION=region S3_ACCESS_KEY_ID=access-id S3_SECRET_ACCESS_KEY=access-key S3_BUCKET=bucket-name S3_PREFIX=prefix

# link db containers
dokku postgres:link www fred
dokku couchdb:link www fred

dokku s3backup:start fred 
```