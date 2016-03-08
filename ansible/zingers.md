
Command mode (default) needs some escapes at times, "" also works

```
ansible -i inventory.txt dockerhosts -a 'sudo apt-get install -y lxc-docker\=1.9.1'
```


The shell module is sometimes more convenient.

```
ansible -i inventory.txt dockerhosts -m shell -a 'sudo puppet agent --disable'
ansible -i inventory.txt dockerhosts -m shell -a 'cd /etc/init.d && for i in docker-*; do echo $i; sudo service $i stop; done'
```
