
ubuntu@bpa-aws1:/data/puppetmaster/environments/aws$ docker exec -it --user postgres postgis bash
postgres@postgis:/$ psql bpam                                                                                                                                                                                      
psql (9.5.2)
Type "help" for help.

bpam=# create extension postgis;
CREATE EXTENSION
bpam=# create extension postgis_topology;
CREATE EXTENSION
bpam=# 
