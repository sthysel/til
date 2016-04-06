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
