[![Docker Repository on Quay](https://quay.io/repository/ppavlov/jenkins-master/status "Docker Repository on Quay")](https://quay.io/repository/ppavlov/jenkins-master)
[![Codefresh build status]( https://g.codefresh.io/api/badges/build?repoOwner=pmpavlov&repoName=docker-stacks&branch=master&pipelineName=jenkins-master&accountName=ppavlov&type=cf-1)]( https://g.codefresh.io/repositories/pmpavlov/docker-stacks/builds?filter=trigger:build;branch:master;service:5ad47cf9ff851700012da140~jenkins-master)


Jenkins Setup
=======================
This repository contains a Docker Swarm setup to create an automated

Extract plugins from your current config and compare:

    curl -sS -u  "admin:password" "http://jenkins.domain/pluginManager/api/json?depth=1" | jq -r '.plugins[].shortName' | tee plugins.txt
 
Create Jenkins service with automated setup
-------------------------------------------

Create the Docker secrets used as Jenkins admin user username and password:

    echo "admin" | docker secret create jenkins-user -
    echo "password" | docker secret create jenkins-pass -

Building the Jenkins image
---------------------------------

Create a Jenkins image with plugins from `plugin.txt`:

    docker build --no-cache -t quay.io/ppavlov/jenkins-master .

Optional: push image to Docker registry:

    docker push quay.io/ppavlov/jenkins-master

Bare in mind that this is how i build it for my repository.

Deploy the stack:

    docker stack deploy -c docker-stack.yml jenkins

Check running services:

    docker stack ps jenkins

Cleaning up afterwards
----------------------

    docker stack rm jenkins
    docker secret rm jenkins-user
    docker secret rm jenkins-pass

How can I see logs from containers

    docker logs <containerId>

How can I see logs from services in stacks

    docker stack services jenkins          # where 'jenkins' is the stack name
    docker service logs -f <SERVICE ID>


