Docker Swarm
============

This is an example only and may not be production-quality. Please submit improvements!

```
$ mkdir -p .secrets
$ openssl rand -base64 32 > .secrets/xtrabackup_password
$ openssl rand -base64 32 > .secrets/mysql_password
$ openssl rand -base64 32 > .secrets/mysql_root_password
$ docker stack deploy -c docker-compose.yml galera
$ docker service ls
(wait for `galera_seed` to be healthy)
$ docker service scale galera_node=2
(wait for both `galera_node` instances to be healthy)
$ docker service scale galera_seed=0
$ docker service scale galera_node=3
```

Note, currently I do not know of a good way to retrieve the DNS name to lookup other IPs so the
`docker-compose.yml` file has `galera_seed,galera_node` hard-coded which would not work unless
`galera` is used as the name of the stack for the `docker stack deploy` command.
