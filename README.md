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
    Postgresql 9.1 (http://postgresapp.com/)
    XCode Developer Tools 4.6.1 (from your app store)
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

Install Chef Client

1. Run the Omnibus installer

    $ curl -L http://www.opscode.com/chef/install.sh | sudo bash

Ensure you enter your local machine's password after running the command above. After entering the password, chef should install.
You should see something like the following

    Downloading Chef for mac_os_x...
      % Total    % Received  % Xferd   Average  Speed    Time     Time      Time   Current
                                       Dload   Upload    Total    Spent     Left   Speed
    100 23.9M  100 23.9M     0     0    944k       0   0:00:26  0:00:26  --:--:--   838k
    Installing Chef

Verify that chef has installed by running
    
    $ chef-client -v

You should see something like this:
    
    Chef: 11.4.0

Check that the following folder stucture is present on your local machine
    
    /opt
       /chef
          /bin
          /embedded
             /bin
             /include
             /lib
             /share
             /ssl

2. Get the .pem files and knife.rb files

    <argha What is the procedure a new dev should follow to obtain these files, and what are the login credentials of the Chef Server?>

Run the following command to ??create??  the knife configuration file
    
    $ knife-configure -initial

..... fill in the next steps

3. Clone the chef repository. It is required if your machine is to interact with the Chef Server
    
    $ git clone git://github.com/opscode/chef-repo.git

If the clone is successful, the following directory structure should be present in the directory into which you cloned the chef repo
    
    chef-repo/
       certificates/
       config/
       cookbooks/
       data_bags
       environments/
       roles/

4. Create the .chef directory to stire the three files that were ??gotten?? from the Chef Server

<i>knife.rb, validation.pem, and xxx.pem where xxx is your username <argha Please verify that this is correct/> </i>

While still in the chef-repo folder, run the following command (sudo is not always required)
    
    $ sudo mkdir .chef

Ensure that the following directory structure is present by running

    $ ls -a

You should see something like
    
    .       .chef       .gitignore  README.md   certificates    config      data_bags   roles
    ..      .git        LICENSE     Rakefile    chefignore  cookbooks   environments

<argha Should we do git ignore on .chef? />



Goal: All devs should know how to and be capable of (i.e. have tools / keys installed) spinning up a new environment.

- Involves understanding chef and knife commands
    
