# uReport - Dev Boostrap

Checking that repo migration worked
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
    $ git clone git@github.com:ureport/bootstrap.git


Some prerequisites:
    
    Rackspace account (we have this set up for you)
    Newrelic account (we have this set up for you)
    Homebrew (https://github.com/mxcl/homebrew/wiki/Installation)
    Python (not 3, 2.7)
    Postgresql 9.1 (http://postgresapp.com/)
    XCode Developer Tools 4.6.1 (from your app store)
    Chef and chef client
    Rackspace client

<b>Postgres</b>

If you have psql (PostgreSQL) 9.0.10 installed, you will need to upgrade to Postgresql 9.1. 

    $brew upgrade psql
    
During this you might run into
 this error:

    error: The following untracked working tree files would be overwritten by merge:
    Library/Formula/libmusicbrainz.rb
    
    Please move or remove them before you can merge.
    Aborting
    Error: Failure while executing: git pull -q origin refs/heads/master:refs/remotes/origin/master

In order to fix this, run command: <code>rm /usr/local/Library/Formula/libmusicbrainz.rb</code>

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
    
    $ git clone git@github.com:ureport/provisioning.git
    
    $ git clone git@github.com:ureport/performance.git
    
    $ git submodule init
    
    $ git submodule update

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

# Run the Omnibus installer

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


# Install knife-rackspace gem
    
    $ gem install knife-rackspace

<b>Copy required files to you Dev machine</b>

    # Copy validation.pem from the chef server at 95.138.169.81 (use the scp command)
        
        /etc/chef

    into your chef directory which is at

        ~/.chef/


    # Obtain the encrypted_data_bag_secret file from <i>one of the developers</i> and copy it to

        ~/.chef/


# In your browser, Go to the Chef Server at http://95.138.169.81:4040/clients and create a client using the "Create" tab

# Enter a client name (your name) and click create. This will generate a private public Key pair that will be associated with the client you create.
# Copy the Private Key into the .pem file under <b>DJ, is the file created before this?</b>
        
        ~/.chef/xxx.pem 

    Where xxx is the name of the client you created

#Add the following to your bash profile at ~/.bash_profile

    # Rackspace credentials
    export RACKSPACE_USERNAME="xxx"
    export RACKSPACE_API_KEY="xxx"
    export NEWRELIC_LICENSE_KEY="xxx"

Substitute the xxx with the rackspace details you obtain from one of the developers

Run the following command to generate the knife configuration file
    
    $ knife configure --initial

    When prompted for chef server url, enter

        'http://95.138.169.81:4000'


Edit knife.rb

knife.rb is found under ~/.chef/knife.rb

#  Open knife.rb and make the following changes :

        validation_key           '~/.chef/validation.pem'
        client_key               '/Users/Nimrod/.chef/nimrod01.pem'

     Copy the following 5 knife attributes into knife.rb 

        knife[:rackspace_api_username] = "#{ENV['RACKSPACE_USERNAME']}"
        knife[:rackspace_api_key] = "#{ENV['RACKSPACE_API_KEY']}"

        knife[:rackspace_version] = 'v2'
        knife[:rackspace_api_auth_url] = "lon.auth.api.rackspacecloud.com"
        knife[:rackspace_endpoint] = "https://lon.servers.api.rackspacecloud.com/v2"

     Add

        encrypted_data_bag_secret '~/.chef/encrypted_data_bag_secret'


Goal: All devs should know how to and be capable of (i.e. have tools / keys installed) spinning up a new environment.

- Involves understanding chef and knife commands
    
