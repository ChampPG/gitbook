# Important

### Starting, Stopping and Removing all

Start the docker-compose yaml file in the current directory the user is in.

```
docker-compose up -d
```

Stop the docker-compose yaml file in the current directory the user is in.

```
docker-compose down
```

Remove all containers along with the related networks, images and volumes.

```
docker-compose down --rmi all --volumes
```

### Active Containers

This command will show the working containers

```
docker-compose ps
```

If Own Cloud was running in docker-compose the output would look like

| Name              | Command                        | State        | Ports                 |
| ----------------- | ------------------------------ | ------------ | --------------------- |
| owncloud\_mariadb | docker-entrypoint.sh --max ... | Up (healthy) | 3306/tcp              |
| owncloud\_redis   | docker-entrypoint.sh --dat …​  | Up (healthy) | 6379/tcp              |
| owncloud\_server  | /usr/bin/entrypoint /usr/b …   | Up (healthy) | 0.0.0.0:8080→8080/tcp |

### OCC Commands

These are tailored for specific applications

This shows how to deploy occ commands to the owncloud container

```
docker-compose exec owncloud occ <command>
```
