# uReport - Dev Boostrap

Contains information and scripts to get a development machine up and running very quickly

# Tech Stack

    Python (not 3, 2.7)
    VirtualEnv (Like rvm for ruby, manages versions of Python)
    Django 1.3
    Postgresql 9.1
    Rackspace
    Chef
    Newrelic


# Developer Machine installation (OS X Mountain Lion)

First install git if you don't already have It, and setup a github account and gravatar image and get access to our team.
if you are using git for the first time, follow these instructions to let you push to the ureport repo https://help.github.com/articles/generating-ssh-keys

Create somewhere to store all the stuff, e.g.

    $ mkdir -p ~/Code/unicef/ureport

First clone this repository so that you can update this doc or the developer-faq with anything you learn!

    $ cd ~/Code/unicef/ureport    
    $ git clone git@github.com:unicef-ureport/bootstrap.git


Some prerequisites:
    
    Rackspace account
    Newrelic account
    Homebrew (https://github.com/mxcl/homebrew/wiki/Installation)
    Python (not 3, 2.7)
    VirtualEnv (Like rvm for ruby, manages versions of Python)
    Postgresql 9.1 (http://postgresapp.com/)
    Chef and chef client
    Rackspace client

Then your pip

    $ sudo easy_install pip
    $ pip install virtualenv

If $ pip install virtualenv fails with the message "Permission Denied", try

    $sudo pip install virtualenv

Go to some folder where you want to store the code and create a folder called “virtualenv”, e.g.

    $ mkdir -p ~/Code/unicef/ureport/virtualenv

Go in there and run virtualenv

    $ cd ~/Code/unicef/ureport/virtualenv
    $ virtualenv --no-site-packages ureport
    
Go back and clone the repos:

    $ cd ..
    $ git clone git@github.com:unicefuganda/ureport.git original-repo
    
    <nimrod: ask us about submodules!!>
    
    $ git clone git@github.com:unicef-ureport/provisioning.git
    
    $ git clone git@github.com:unicef-ureport/performance.git

Activate your virtualenv so ureport can run on the python instance in the virtualenv

    $ source ~/Code/unicef/ureport/virtualenv/ureport/bin/activate
    
Configure your python environment     
    
    $ cd ~/Code/unicef/ureport/original-repo/
    $ pip install -r pip-requires.txt
    
You can see if this works by 

    $ pip freeze
    
It should show you all the libraries that are in pip-install.txt

Now make sure you have postgress installed and running...

    $ lsof -i:5432
    You should see something like:
    COMMAND    PID USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
    postgres 72677 XXXX    5u  IPv6 0x1e7355b40b608055      0t0  TCP
    localhost:postgresql (LISTEN)
    postgres 72677 XXXX    6u  IPv4 0x1e7355b417851705      0t0  TCP
    localhost:postgresql (LISTEN)
    postgres 72677 XXXX    7u  IPv6 0x1e7355b410d27c75      0t0  TCP
    localhost:postgresql (LISTEN)
    
    
You should also be able to do :

    $ psql
    
And it should give you a db console.


... Now all the chef and rackspace stuff

Goal: All devs should know how to and be capable of (i.e. have tools / keys installed) spinning up a new environment.

- Involves understanding chef and knife commands
    
