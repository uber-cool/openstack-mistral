# Run Openstack Mistral as Docker container

This guide outlines how to run mistral on docker and create a simple workflow and executes it.

## Pre-requisites
* Docker or docker toolbox installed. For beginners docker toolbox is great way to start.
https://docs.docker.com/toolbox/toolbox_install_windows/

## Steps to start Mistral in Docker
1. Start the Docker Quickstart Terminal. This will start the VM required for docker and start docker daemon on it.
Once completed you'll be connected to the docker terminal running on the VM.
Run below command to check if you are successfully connected to Docker terminal
     ```
   docker images
     ```
   This will list images if there are any.
2. Mistral uses RabbitMQ as queue manager. We'll first download RabbitMQ image and run it
   ```
   docker run -d --name my_rabbitmq rabbitmq
   ```
   If the image is already not present you'll see a message like:<br/>
   _Unable to find image 'rabbitmq:latest' locally_ <br/>
   After few moments docker will start to download the image from repository. It'll also create a container from this image and run it.
3. Run below command to verify if the RabbitMQ has started, the output should show a running container _my_rabbitmq_
   ```
   docker ps
   ```
4. Mistral images are not available in repository. You need to build the image yourself as described in the link below:<br/>
   https://docs.openstack.org/mistral/ocata/guides/installation_guide.html#mistral-and-docker<br/>
   This page also has link to pre-built image from where you can directly download the image.
   https://tarballs.openstack.org/mistral/images/mistral-docker.tar.gz
5. Move to the path where you have built/downloaded the image and run below command:
   ```
   docker load -i mistral-docker.tar.gz
   ```
   You'll see output like this:
   ```
   $ docker load -i mistral-docker-latest.tar.gz
   fccbfa2912f0: Loading layer [==================================================>]  116.9MB/116.9MB
   e1a9a6284d0d: Loading layer [==================================================>]  15.87kB/15.87kB
   ac7299292f8b: Loading layer [==================================================>]  14.85kB/14.85kB
   a5e66470b281: Loading layer [==================================================>]  5.632kB/5.632kB
   a8de0e025d94: Loading layer [==================================================>]  3.072kB/3.072kB
   ae83ae36e142: Loading layer [==================================================>]  6.162MB/6.162MB
   cc54b09a1284: Loading layer [==================================================>]    449MB/449MB
   34aa25b2be8f: Loading layer [==================================================>]  54.49MB/54.49MB
   4d3549052301: Loading layer [==================================================>]  5.632kB/5.632kB
   35f91544247a: Loading layer [==================================================>]  201.5MB/201.5MB
   70923787fab6: Loading layer [==================================================>]  4.608kB/4.608kB
   00e7c6811483: Loading layer [==================================================>]  9.143MB/9.143MB
   f355cab9bc6c: Loading layer [==================================================>]  86.02kB/86.02kB
   Loaded image: mistral:latest
   ```
6. Verify that the image is loaded successfully, below command should list mistral image
   ```
   docker images
   ```
7. Run a container with this image, you need to link this container with already running RabbitMQ container
   ```
   docker run -d  --link my_rabbitmq:my_rabbitmq -p 8989:8989 --name my_mistral mistral
   ```
   Now there should be two containers running (docker ps), my_mistral and my_rabbitmq
8. By this time your mistral instance is ready for your commands. Follow this link to create and execute your first workflow.