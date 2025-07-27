# lucky
```bash
docker compose up -d
```
127.0.0.1:16601
lkudsurf
Hu2578925789

dnspod id token
586087
b0d0ba95dc8f6e8e3b348686a27101a4

# nextcloud
./nextcloud/config/ports.conf
```bash
docker compose up -d

docker exec nextcloud su -s /bin/sh www-data -c "php occ config:system:set trusted_domains 1 --value='nextcloud.lkudsurf.online'"

docker exec nextcloud su -s /bin/sh www-data -c "php occ config:system:set overwriteprotocol --value='https'"

docker exec nextcloud su -s /bin/sh www-data -c "php occ config:system:set forwarded_for_headers --value='HTTP_X_FORWARDED_FOR'"
```

# wireguard
```bash
docker compose up -d
```