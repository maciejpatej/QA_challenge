##Task 1
```
1. You are asked to install docker and docker-compose on a remote server
   accessible using the hostname `remote-server-ip`. You have access to the
   private key file `my-key-pair.pem`. You know the remote machine is running
   Debian Linux distribution. What are the commands you would run to install the
   docker and docker-compose binaries in the remote machine.
```
   

##Answer (Example for Linux-based client):

The most straightforward solution requires an SSH tool(`ssh`), `my-key-pair.pem` file (assumed it is present in client homedir), hostname (`remote-server-ip`, assumed no virtualization problems :) ) and the username (assumed `user`). 

1. Set correct permissions for the .pem file if not already set:
```
chmod 400 mykey.pem
``` 

2. Connect to the remote server via SSH:
```
ssh -i my-key-pair.pem user@remote-server-ip
```

3. Install Docker using official guide. Source: [Docker docs](https://docs.docker.com/engine/install/debian/):

#Install necessary components for the installation of the repository
```
sudo apt-get update
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

#Add Docker GPG key
```
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

#Setup Docker repository for stable release
```
echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

#Update and install Docker Engine and containerd
```
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```


##Problem 2

Checking the virtual memory size (allocated memory for the process) and resident set size (amount of memory actually used by the process) for docker containers isn't as obvious as in the standard linux process. 

1. We need to find the container ID (assuming we already accessed the machine hosting the containers):
```
docker inspect <container name> -f "{{.ID}}"
```

2. Display the stats file (`memory.stat`) of the container:
```
cat /sys/fs/cgroup/memory/docker/<docker ID we just found in step 1>/memory.stat
```
There should be a clear statement of the RSS, while the real VSZ value would be the sum of RSS, cache and swap. 

2.1 Values for containers in the Kubernetes cluster can be seen in the more practical manner by using the command:
```
kubectl top pods
```

We should see the table with RSS and virtual size listed.