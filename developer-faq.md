## Developer FAQ

A list of questions that people ask when they join the team!


### What are submodules and how do they work?

<nimrod: you can fill this in when you understand them:)>


#### What does $ virtualenv --no-site-packages do?
	Will ensure that the python you install for ureport doesn't affect your global python installation. 
	In effect, you can have many applications on your machine, each on a separate version of python without running into conflicts.
	For more information, see http://www.virtualenv.org/en/1.7.2/#what-it-does


#### How do you activate your virtual environment
	
	$ source /path to your ureport code/virtualenv/bin/activate

You should then see <b>(ureport)</b> before your commandline prompt. 


#### What does cat <filename> | grep <search_text> do?
	
	Serches within the file for the search_text


#### Setting up to run the server locally

    brew install nginx Note you should make sure brew is up to date (brew doctor)
    
    brew install uwsgi
    
    brew install uwsgi-plugin-python
        
You will need the nginx conf and the ureport nginx conf. The files you need are in this dir. 

    vim /usr/local/etc/nginx/nginx.conf

You need to link ureport into where nginx can see it...

    ln -s ${UREPORT_HOME} /usr/local/var/www/ureport
    
To reload configuration just type

    nginx -s reload
    

#### Geoserver Layer setup debugging

NullPointer Exception: Have you requested for a property that doesn't exist?
Look into
    <code>/var/lib/geoserver_data/workspaces/unicef/geoserver/{<LAYER_NAME_FILE>}</code>
and ensure that the <name> and <native_name> tags both contain the same string.

Error occurred getting features Schema 'http://unicef.org/ureport:xxxx' does not exist when 
setting up a layer for categorical polls. Look in the same place as shown above for the features.xml
file for the layer and ensure that under the <virtualTable> entry has the same name as the name of
the layer you have created

Geoserver does not show data in geoserver db. It could be that it cannot connect to the DB. Check the
geoserver.log to find out if it is complaining about failure to connect to the DB. If it is the case,
ensure that the 'datastore.xml' is configured correctly.


#### Where are the logs??

<b>tomcat:</b> /usr/local/Cellar/tomcat/7.0.39/libexec/logs/catalina.out

<b>geoserver:</b> /var/lib/geoserver_data/logs/geoserver.log

<b>uwsgi:</b> /var/log/uwsgi/app/ureport.log (Comes in handy when uwsgi restarts but you still get an nginx
502 Bad Gateway



#### Exporting Shape Files into geoserver db.

Get the .zip file of the shape files data and extract it to the directory you want to work from. Any directory
will do.

If you have a geoerver db setup already and you only need to update the shape files in it,

cd into the directory into which you extracted the .zip containing the shape files and run a command similar to 
<code>ogr2ogr -f "PostgreSQL" -t_srs EPSG:900913 PG:"host=localhost user=postgres dbname=geoserver" Adm3_Counties_coarse.shp -nlt multipolygon -nln southsudan_districts2013 </code>

Ensure to replace the arguments in the command with the appropriate db credentials, shape file (.shp) and
the correct name you want your db table that will contain the shape files to be called.

If you have no geoserver db set up at all, Look at the script in ureport_project/rapidsms_geoserver/setup.sh
to see the things you have to do to set it up from your shape files

<br>
#### <u>Run a specific recipe/cookbook on a chef node</u>

chef-client -o 'role[networking]' --once

<br>
#### Decypting / Encrypting chef data bags

http://docs.opscode.com/essentials_data_bags_encrypt.html

<br>
#### git keeps asking for a passphrase for any pull or push

http://stackoverflow.com/questions/10032461/git-keeps-to-ask-me-for-ssh-key-passphrase

<br>
#### Load locations into ureport db

<code>./manage.py laoddata locations --settings=YOUR_SETTINGS_FILE</code>

<br>
#### How to simulate responses to polls

Ensure you have a contact with the backend, identity and group properties set up. 
<code>http://localhost:8088/router/receive?message=No&backend=console&sender=10</code>
'Sender' corresponds to the contact's identity.

<br>
#### Useful commands
<ul>
   <li> CMD+k : Clear logs
</ul>

