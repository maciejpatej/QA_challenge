# QA DevOps Engineer challenge


## Problem statement

1. You are asked to install docker and docker-compose on a remote server
   accessible using the hostname `remote-server-ip`. You have access to the
   private key file `my-key-pair.pem`. You know the remote machine is running
   Debian Linux distribution. What are the commands you would run to install the
   docker and docker-compose binaries in the remote machine.
   
2. Once you have installed the packages, you are asked to start the docker
   service and check if the process is running. Tell us how you would check the
   memory allocated and used by the docker process (hint: RSS and VSZ).

3. Your company's data scientist just finished working on an application and
   they want the code to be deployed to the Kubernetes cluster that you are
   maintaining. They went ahead and wrote the Dockerfile and docker-compose file
   to give you an idea of how they want the tool to be deployed. Your task is
   to deploy it as scalable pods that can be accessed at the URL
   `streaming.quickalgorithm.com`. Please write the Kubernetes configuration
   files for the aforementioned codebase, specifying the assumptions that were
   taken during the process.
   
   Your data scientist's code can be found [here](https://github.com/dmontag23/qa-streaming-pipeline-challenge).
 
   

## How to submit the solution

Please create a public git repo on a hosting service of your choice(github,
gitlab, etc.) and add solutions to the challenges to it as you deem fit. Share
the repo with us before the deadline agreed upon.
