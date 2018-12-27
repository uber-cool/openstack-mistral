# Run Openstack Mistral as Docker container



## Pre-requisites
* Docker or docker toolbox installed. For beginners docker toolbox is great way to start.
https://docs.docker.com/toolbox/toolbox_install_windows/

## Steps to start Mistral in Docker
1. Mistral images are not available in repository. You need to build the image yourself as described in the link below:<br/>
   https://docs.openstack.org/mistral/ocata/guides/installation_guide.html#mistral-and-docker<br/>
   This page also has link to pre-built image from where you can directly download the image.
   https://tarballs.openstack.org/mistral/images/mistral-docker.tar.gz
2. Move to the path where you have built/downloaded the image and run below command:
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
3. Verify that the image is loaded successfully, below command should list mistral image
   ```
   docker images
   ```
4. Run a container with this image, you need to link this container with already running RabbitMQ container
   ```
   docker run -d -p 8989:8989 --name mistral_all mistral:latest
   ```
   This command will create a new container named _mistral_all_. You can verify this with `docker ps` command
   ```
   CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                    NAMES
   54b89e5ccbdf        mistral             "/usr/bin/tini -- /b…"   2 minutes ago       Up 2 minutes        0.0.0.0:8989->8989/tcp   mistral_all
   ```
5. By this time your mistral instance is ready for your commands. Follow this link to create and execute your first workflow.
