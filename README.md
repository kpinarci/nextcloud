Automated docker Nextcloud for Nginxproxymanager.

Prerequisites

In order to use this compose file (docker-compose.yml) you must have:

1. Docker
2. Docker-compose
3. Docker-compose Nginxproxymanger https://github.com/jc21/nginx-proxy-manager

How to use

1. Clone this repo:

https://github.com/kpinarci/nextcloud.git

2. Rename our nc.env file it to .env and change our preferences. 

3. Check your configuration.

$ docker-compose --env-file .env config

4. If the configurations is correct, then start the container.

$ docker-compose --env-file .env up -d

5. Overwrite protocol to https.

$ docker exec --user www-data nextcloud-app php occ config:system:set overwriteprotocol --value="https"

6. Add "default_phone_region code".

$ docker exec --user www-data nextcloud-app php occ config:system:set default_phone_region --value="DE"

7. Add a new domain to “trusted domains”.

$ docker exec --user www-data nextcloud-app php occ config:system:set trusted_domains 1 --value=<YourNextcloudDomain>

8. If Nextcloud need SVG for php-imagick, you can install with this:

$ docker exec -it --user root nextcloud-app apt install imagemagick

9. If Nextcloud has problems with CalDav and CalDav, then you need to add the following line to your proxy settings:

NGINX
location /.well-known/carddav {
    return 301 $scheme://$host/remote.php/dav;
}

location /.well-known/caldav {
    return 301 $scheme://$host/remote.php/dav;
}





