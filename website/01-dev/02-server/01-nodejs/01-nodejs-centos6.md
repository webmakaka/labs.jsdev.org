---
layout: page
title: Node.js installation on centos 6.X
permalink: /server/nodejs/installation-on-centos-6/
---

# Node.js installation on centos 6.X

    # curl -sL https://rpm.nodesource.com/setup | bash -
    # yum install -y nodejs npm

    # node --version
    v0.10.32

    # npm --version
    1.4.28

    # npm install -g bower

    # bower --version
    1.3.12

<br/>

    # npm install -g nodemon

<br/>

### Example, how to run an application on node.js server:

    # mkdir -p /projects/myproject

<br/>

    # useradd developer

    # chown -R developer /projects

    # su - developer

<br/>

    $ vi ~/.bowerrc
    {
    	"directory": "public/vendor/lib"
    }

<br/>

### Example how to run oracle jet application on node.js server

    $ cd /projects/myproject/

<br/>

    $ npm install express-generator -g
    $ express oraclejetwithnodejs

<br/>

    $ cd myproject/oraclejetwithnodejs/public/
    $ git clone https://github.com/oracle-jet/work-better-jet

<br/>

    $ cd /projects/myproject/oraclejetwithnodejs
    $ vi app.js

    replace

    app.use(express.static(path.join(__dirname, 'public')));

on

    app.use(express.static(path.join(__dirname, 'public/work-better-jet')));

<br/>

    $ npm start

<br/>

browser --> http://host:3000
