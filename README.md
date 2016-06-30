# Git
## Tagging

```
git tag -a v1.4 -m "my version 1.4"
git push --tags
```
-a add a new tag

Tags need to be explicitly pushed.

## Spliting repos appart

1. Clone original repo
1. Remove original origin
1. Filter out the rest using *--subdirectory-filter* (or any other directive)
1. Clean out the original refs
1. Make new origin repo 
1. Push


Filter recipe example:
```
git filter-branch --subdirectory-filter vim -- master
git for-each-ref --format='delete %(refname)' refs/original | git update-ref --stdin
git reflog expire --expire=now --all
git gc --prune=now
git remote add origin git@github.com:sthysel/dotvim.git
```
# aws cli 

```
aws --profile=tmeintjes s3 ls --summarize --recursive s3://brl-syd/arundo_donax
aws --profile=tmeintjes s3 --dryrun --recursive mv s3://brl-syd/arundo_donax s3://brl-glacier-syd/1day/arundo_donax/
```

Command mode (default) needs some escapes at times, "" also works

```
ansible -i inventory.txt dockerhosts -a 'sudo apt-get install -y lxc-docker\=1.9.1'
```


The shell module is sometimes more convenient.

```
ansible -i inventory.txt dockerhosts -m shell -a 'sudo puppet agent --disable'
ansible -i inventory.txt dockerhosts -m shell -a 'cd /etc/init.d && for i in docker-*; do echo $i; sudo service $i stop; done'
```
# apt-get good practice 

Install specified version, reluctantly.
```
sudo apt-get install lxc-docker=1.9.1 --assume-no
```

# Common ceph actions

```
ceph osd set noout
ceph osd unset noout
ceph health

```

# Openstack nova 

```
nova list
nova start sshbounce
```

# Docker proxy containers 

These proxies are hosted in containers. The proxies caches apt (squid) and pip (pypi)
packages and improves image building time.

## http squid proxy
```
 systemctl start squid.service
 systemctl status squid.service
```


## devpi pip proxy
```
 systemctl status devpi.service
 systemctl start devpi.service
```

```
$ docker ps                         
CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                                                                          NAMES
63871f5c9273        muccg/devpi:latest             "/docker-entrypoint.s"   7 minutes ago       Up 7 minutes        0.0.0.0:3141->3141/tcp                                                         devpi.service
4c9b20ab37ac        muccg/squid-deb-proxy:latest   "/docker-entrypoint.s"   7 minutes ago       Up 7 minutes        0.0.0.0:3128->8000/tcp                                                         squid.service
```

# Cachebusting to force re-downloads or git clones

A pattern to force the docker cache to be invallid

In Dockerfile
```
ARG CACHEBUST=1
RUN git clone https://github.com/octocat/Hello-World.git
```

Used like so
```
docker build -t your-image --build-arg CACHEBUST=$(date +%s) .
```

For git
```
export CACHEBUST=$(git ls-remote https://username@bitbucket.org/username/myRepo.git | grep refs/heads/develop | cut -f 1) && echo $CACHEBUST
docker build -t myDockerUser/myDockerImage \
   --build-arg blah=blue \
   --build-arg CACHEBUST=$CACHEBUST \

```

# vim-fu
## history
```
'.
''
g;
g.
```

## General

I want to                               | tell vim
---                                     | ---
delete buffer                           | :bd <text>
select                                  | v                                    
select row(s)                           | SHIFT + v                            
select blocks (columns)                 | CTRL  + v                            
indent selected text                    | >                                    
unindent selected text                  | <                                    
list buffers                            | :ls                                  
open buffer                             | :b <buffer name>                    
print                                   | :hardcopy                            
open a file                             | :e /path/to/file.txt                 
sort selected rows                      | :sort                                
search for word under cursor            | *                                    
open file under cursor                  | gf                                   
  (absolute path or relative)           |                                      
format selected code                    | =                                    
select contents of entire file          | ggVG                                 
convert selected text to UPERCASE       | U                                    
convert selected text to lowercase      | u                                    
invert case of selected text            | ~                                    
convert tabs to spaces                  | :retab                               
start recording a macro                 | qX (X = key to assign macro to)      
stop recording a macro                  | q                                      
playback macro                          | @X (X = key macro was assigned to)   
replay previously played macro [1]      | @@                                   
auto-complete a word you are typing [2] | CTRL + n                             
bookmark current place in buffer        | mX (X = key to assign bookmark to)   
jump to bookmark                        | `X (X = key bookmark was assigned to 
                                        |     ` = back tick/tilde key)         
show all bookmarks                      | :marks                               
delete a bookmark                       | :delm X (X = key bookmark to delete)  
delete all bookmarks                    | :delm!                                
split screen horizontally               | :split                               
split screen vertically                 | :vsplit                              
navigating split screens                | CTRL + w + j = move down a screen    
                                        | CTRL + w + k = move up a screen      
                                        | CTRL + w + h = move left a screen    
                                        | CTRL + w + l = move right a screen   
close all other split screens           | :only                                
center text at cursor                   | :zz                                 
move cursor line to top                 | :zt                                 
move cursor line to bottom              | :zb                                 
 
[1]  - As with other commands in vi, you can playback a macro any number of times.
     The following command would playback the macro assigned to the key `w' 100
     times: 100@w

[2] - Vim uses words that exist in your current buffer and any other buffer you 
     may have open for auto-complete suggestions.


# Recursive rename

```
$ find . -name *.txt | xargs rename "s/sums.txt/sums.md5/g"
```

# Perl rename
Match gene indexi and usage of named groups.

```
$ rename 's/([GATC]{8})_([GATC]{8})/$1-$2/g' *
```

# Django
## migrations

When clearing out old migrations, remeber that the new built-in migration system is 
only switched on when a "migrations" module exists in the app.
```
migrations/__init__.py
```

It would have been nice if Django were more explicit with its erorr messages about that...
## django import-export

## Resource
    * import_data(dataset)
        * RESULT
        * before_import(dataset) <H>
        * for each row in dataset:
            * get_or_init_instance(row)
                * get || init
            * for_delete(instance)
            * import_obj(instance, row)
                * for each field in Resource:
                * import_field(field, instance, data)
                    * if (field.attribute && field.column_name)
                        * field.save(instance)
                            attribute = field.clean(data)
            * skip_row(updated_object, original_object)
            * before_save_instance(instance) <H>
            * save_instance(instance) <H>
            * after_save_instance(instance) <H>
            * save_m2m()
            * Add row result to RESULT


## hydrate

For some reason dehydrate is also called on import, why ?

```
def dehydrate_lat(self, resource):
    if resource.site:
        return resource.site.get_lat()
```

# Postgres

## Geo Django
```
ubuntu@bpa-aws1:/data/puppetmaster/environments/aws$ docker exec -it --user postgres postgis bash
postgres@postgis:/$ psql bpam                                                                                                                                                                                      
psql (9.5.2)
Type "help" for help.

bpam=# create extension postgis;
CREATE EXTENSION
bpam=# create extension postgis_topology;
CREATE EXTENSION
bpam=# 

```

Here's a handy PostgreSQL feature for testing things such as migrations,
data munging scripts, etc.

When you create a new database, it can be created from a template
database. This is usually a lot faster than remaking the database from
scratch.

For example:
```
createdb -O myuser -T myapp myapp2
DBNAME=myapp2 django-admin my_script
dropdb myapp2
```
You can also rename databases with psql:

```
echo "alter database myapp rename to myapp_template;" | psql postgres
```

References:

- https://www.postgresql.org/docs/9.5/static/app-createdb.html
- https://www.postgresql.org/docs/9.5/static/sql-createdatabase.html
- https://www.postgresql.org/docs/9.5/static/sql-alterdatabase.html


# Sequence filenames regex

```
(?P<id>\d{4,6})_
(?P<extraction>\d)_
(?P<libary>PE|MP)_
(?P<size>\d*bp)_
MM_
(?P<vendor>AGRF|UNSW)_
(?P<plate>\w{9})_
(?P<index>[G|A|T|C|-]*)_
(?P<lane>L\d{3})_
(?P<read>R[1|2])\.fastq\.gz
```

Mathes 

```
21655_1_PE_680bp_MM_AGRF_H3VJJBCXX_GTAGAGGA_L001_R2.fastq.gz
21655_1_PE_680bp_MM_AGRF_H3VJJBCXX_GTAGAGGA_L002_R1.fastq.gz
21655_1_PE_680bp_MM_AGRF_H3VJJBCXX_GTAGAGGA_L002_R2.fastq.gz
21675_1_MP_700bp_MM_UNSW_HKL5CBCXX_TAAGGCGA-CTCTCTAT_L001_R1.fastq.gz
21675_1_PE_700bp_MM_UNSW_HKL5CBCXX_TAAGGCGA-CTCTCTAT_L001_R2.fastq.gz
21675_1_PE_700bp_MM_UNSW_HKL5CBCXX_TAAGGCGA-CTCTCTAT_L002_R1.fastq.gz

```
