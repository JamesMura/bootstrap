# uReport - Dev Boostrap

Contains information and scripts to get a development machine up and running very quickly

# Tech Stack

    Python (not 3, 2.7)
    VirtualEnv (Like rvm for ruby, manages versions of Python)
    Django 1.3
    Postgresql 9.1


# Developer Machine installation (OS X Mountain Lion)

Some prerequisites:

    Homebrew (https://github.com/mxcl/homebrew/wiki/Installation)
    Python (not 3, 2.7)
    VirtualEnv (Like rvm for ruby, manages versions of Python)
    Postgresql 9.1 (http://postgresapp.com/)


Then your pip

    $ sudo easy_install pip
    $ pip install virtualenv

Go to some folder where you want to store the code and create a folder called “virtualenv”, e.g.

    $ mkdir -p ~/Code/unicef/virtualenv

Go in there and run virtualenv

    $ cd ~/Code/unicef/virtualenv
    $ virtualenv --no-site-packages ureport
    
Go back and clone the repo:

    $ cd ..
    $ git clone git@github.com:unicefuganda/ureport.git ureport-repo
    $ cd ureport-repo/ureport-project
    $ pip install -r pip-requires.txt


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
    
    
