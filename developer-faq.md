# Developer FAQ

A list of questions that people ask when they join the team!

# FAQ

## What are submodules and how do they work?

<nimrod: you can fill this in when you understand them:)>

##What does $ virtualenv --no-site-packages do?
	Will ensure that the python you install for ureport doesn't affect your global python installation. 
	In effect, you can have many applications on your machine, each on a separate version of python without running into conflicts.
	For more information, see http://www.virtualenv.org/en/1.7.2/#what-it-does

# How do you activate your virtual environment
	
	$ source /path to your ureport code/virtualenv/bin/activate

You should then see <b>(ureport)</b> before your commandline prompt. 

# What does cat <filename> | grep <search_text> do?
	
	Serches within the file for the search_text