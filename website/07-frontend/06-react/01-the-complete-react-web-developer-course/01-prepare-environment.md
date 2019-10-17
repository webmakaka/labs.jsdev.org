---
layout: page
title: React.js - The Complete React Web Developer Course (2nd Edition)
permalink: /frontend/react/the-complete-react-web-developer-course-2nd-edition/prepare-environment/
---

# The Complete React Web Developer Course (2nd Edition)

<br/>

## Prepare Environment for Development


<br/>

    $ project_name=the-complete-react-web-developer-course-2nd-edition
    $ echo $project_name
    the-complete-react-web-developer-course-2nd-edition

<br/>

    $ project_folder=~/projects/dev/js/react/
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

    $ source ~/.bash_profile

<br/>

CTRL + D

<br/>

    # mkdir -p /usr/local/lib/node_modules/
