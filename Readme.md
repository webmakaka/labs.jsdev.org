# [labs.jsdev.org](//labs.jsdev.org) source codes


<br/>

### Run labs.jsdev.org on localhost

    # vi /etc/systemd/system/labs.jsdev.org.service

Insert code from jsdev.org.service
    
    # systemctl enable labs.jsdev.org.service
    # systemctl start  labs.jsdev.org.service
    # systemctl status labs.jsdev.org.service


http://localhost:4008


<br/>

### To run jsdev.org on your local server, you can do next:

**Install Docker**

Then

    docker pull marley/centos6-for-dev
    docker run -i -t –rm -p 80:8080 –-name jsdev-org marley/centos6-for-dev /bin/bash


    source ~/.bash_profile
    cd /projects
    git clone --depth=1 https://bitbucket.com/jsdev-org/labs.jsdev.org
    cd labs.jsdev.org
    gem install jekyll
    jekyll serve --watch --host 0.0.0.0 --port 8080


and connect to localhost.
