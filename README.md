# nixos-wiki-infra

This project contains the setup of https://wiki.nixos.org

## Examples

Checkout [./targets/nixos-wiki.nixos.org]() for an example terraform deployment on hetzner cloud.

## Downloading a dump of the wiki

This is useful if you want to run your own instance.
Every day an xml dump is updated here:

https://wiki.nixos.org/wikidump.xml.zst

## Restoring from a backup (wiki admins only)

```
$ systemctl stop phpfpm-mediawiki.service
$ borg-job-wiki list
$ borg-job-wiki mount u391032-sub1@u391032.your-storagebox.de:wiki.nixos.org/repo::wiki-wiki-2024-04-01T12:40:37 /tmp/restore
$ ls -la /tmp/restore/var/lib/mediawiki/backup/
$ sudo dropdb db
$ sudo -u postgres dropdb mediawiki
$ systemctl restart postgresql.service
$ sudo -u postgres pg_restore -d mediawiki < /tmp/restore/var/lib/mediawiki/backup/db
$ systemctl start phpfpm-mediawiki.service
$ ls -la /tmp/restore/var/lib/mediawiki-uploads/
$ umount /tmp/restore/
```

## Join our Matrix

https://matrix.to/#/#wiki:nixos.org
