Run two sets of applications of your choice on different docker daemons
For this we can use docker context to access the remote hosts, First create a context that will hold the connection path to it.
docker context create remote ‐‐docker “host=ssh://user@remotemachine”
Than switch to that context using 
docker context use remote
We can run docker-compose and specify the context “remote” to automatically target the remote host. If no context is specified, docker-compose will use the current context just like the Docker CLI.
docker-compose up -d
target the remote host
docker-compose ‐‐context remote up -d
