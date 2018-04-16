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

Deploy the stack:

    docker stack deploy -c docker-stack.yml jenkins

Check running services:

    docker stack ps jenkins
