```
scp /opt/marzban/backup/backup_20250527215845.tar.gz user@new-server:/tmp/

```
		

```
# Extract the backup
mkdir -p /tmp/marzban_restore
tar -xzvf /tmp/backup_20250527215845.tar.gz -C /tmp/marzban_restore

```

```
cp /tmp/marzban_restore/marzban_data/db.sqlite3 /var/lib/marzban/

```

```
cp /tmp/marzban_restore/marzban_data/xray_config.json /var/lib/marzban/

```

```
cp /tmp/marzban_restore/docker-compose.yml /opt/marzban/

```

```
cp /tmp/marzban_restore/.env /opt/marzban/

```

```
marzban up
```

```
marzban logs
```
