### What's the difference between `up`, `run` and `start`
Typically, you want `docker-compose up`. Use `up` to start or restart all the services defined in a `docker-compose.yml`. In the default “attached” mode, you see all the logs from all the containers. In “detached” mode (-d), Compose exits after starting the containers, but the containers continue to run in the background.   

The `docker-compose ru`n command is for running “one-off” or “adhoc” tasks. It **requires the service name** you want to run and only starts containers for services that the running service depends on. Use run to run tests or perform an administrative task such as removing or adding data to a data volume container. The run command acts like docker run -ti in that it opens an interactive terminal to the container and returns an exit status matching the exit status of the process in the container.   

The `docker-compose start` command is useful only to restart containers that were previously created, but were stopped. It never creates new containers.
### docker-compose run
https://docs.docker.com/compose/reference/run/
经常会在makefile里面看到，`docker-compose run ..`
```
Usage:
    run [options] [-v VOLUME...] [-p PORT...] [-e KEY=VAL...] [-l KEY=VALUE...]
        SERVICE [COMMAND] [ARGS...]

Options:
    -d, --detach          Detached mode: Run container in the background, print
                          new container name.
    --name NAME           Assign a name to the container
    --entrypoint CMD      Override the entrypoint of the image.
    -e KEY=VAL            Set an environment variable (can be used multiple times)
    -l, --label KEY=VAL   Add or override a label (can be used multiple times)
    -u, --user=""         Run as specified username or uid
    --no-deps             Don't start linked services.
    --rm                  Remove container after run. Ignored in detached mode.
    -p, --publish=[]      Publish a container's port(s) to the host
    --service-ports       Run command with the service's ports enabled and mapped
                          to the host.
    --use-aliases         Use the service's network aliases in the network(s) the
                          container connects to.
    -v, --volume=[]       Bind mount a volume (default [])
    -T                    Disable pseudo-tty allocation. By default `docker-compose run`
                          allocates a TTY.
    -w, --workdir=""      Working directory inside the container
 ```
 比如
 `docker-compose run web bash` 其中web对应的就是SERVICE, `bash`
 
 ### What's the difference between `docker-compose build` and `docker build`?
 在这里感受一下 `build`是build image, `run`是run service
 `docker-compose` can be considered a wrapper around the docker cli. It uses a filed called `docker-compose.yml` in order to retrieve parameteres.   
 So basically `docker-compose` build will read your `docker-compose.yml`, look for all services containing the `build: ` statement and run a `docker build` for each one.   
 
