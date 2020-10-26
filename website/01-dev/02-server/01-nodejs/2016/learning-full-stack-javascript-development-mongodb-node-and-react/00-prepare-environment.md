---
layout: page
title: Learning Full-Stack JavaScript Development MongoDB, Node and React
permalink: /server/nodejs/2016/learning-full-stack-javascript-development/prepare-environment/
---

# Learning Full-Stack JavaScript Development: MongoDB, Node and React

<br/>

## Prepare Environment for Development

<br/>

    $ project_name=learning-full-stack-javascript-development-mongodb-node-and-react
    $ echo $project_name
    learning-full-stack-javascript-development-mongodb-node-and-react

<br/>

    $ project_folder=~/projects/dev/js/nodejs/
    $ echo $project_folder
    $ mkdir -p ${project_folder}/${project_name}

<br/>

    $ docker run -it \
    -p 80:8080 -p 1337:1337 -p 3000:3000 -p 4000:4000 -p 5000:5000 -p 6000:6000 -p 7000:7000 -p 8000:8000 -p 9000:9000 \
    --name ${project_name} \
    -v ${project_folder}/${project_name}:/project \
    node \
    /bin/bash

<br/>

    # apt-get update
    # apt-get install -y vim git

<br/>

    # mkdir -p /usr/local/lib/node_modules/

<br/>

    # username=developer

    # adduser --disabled-password --gecos "" ${username}

    # chown -R ${username} /project/

    # su - ${username}

<br/>

    $  vi ~/.bashrc

<br/>

In the bottom I am add

    ###############################
    # USER DEFINED
    . ~/.bash_profile
    ###############################

<br/>

    $ echo "export PS1='$ '" >> ~/.bash_profile
    $ echo 'export PATH=$PATH:./node_modules/.bin' >> ~/.bash_profile

    $ source ~/.bash_profile
