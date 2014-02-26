install
=======

An installer and maintenance package for The Parbake Project

## Configuration
The sample configuration file is named config.default. Copy this to a file named config and set the proper 
configuration values.

````
PROJECT_PATH="/var/www/parbake.org" #Path to the project, the folder into which the app directory will be deployed
APACHE_PROCESS="www-data" #Apache process, probably www-data
USER="user" #probably the user name you used to log on to this machine with
AS='sudo' #sudo or root depending on the OS Ubuntu would probably be sudo, Debian would probably be root

#All of the repositories that make up your project
REPOS="
	--App
	/,app,git@github.com:parbake/parbake.git,write
	--Config
	/app,Config,git@github.com:parbake/Config.git,write
	--Parbake_Plugins
	/app/Plugin,Contents,git@github.com:parbake/Contents-plugin.git,write
	/app/Plugin,Users,git@github.com:parbake/Users-plugin.git,write
	/app/Plugin,Utilities,git@github.com:parbake/Utilities-plugin.git,write
	--Third_Party_Plugins
	/app/Plugin,AuditLog,git@github.com:jasonsnider/CakePHP-Audit-Log-Plugin.git,read
	--CakePHP_and_CakeDC_Plugins
	/app/Plugin,Tags,https://github.com/CakeDC/tags.git,read
	/app/Plugin,Search,https://github.com/CakeDC/search.git,read
	/app/Plugin,DebugKit,https://github.com/cakephp/debug_kit.git,read
	--Vendors
	/app/Vendor,HtmlPurifier,git://repo.or.cz/htmlpurifier.git,read
"
````

### The Repos array
The REPOS array is really just a comma and whitespace delimited string designed to be parsed a multidimensional array.
The first delimiter is whitespace, each white space delimited element represents a git repository. The first element
you'll notice in the example above is --App, a element beginning with -- represents a comment, comments may not have 
whitespace (as this is a delimiter) instead we use underscores as whitespace.

Each element is further delimited by commas and contains 4 sections. The first being the location in to which a 
repository will be cloned. The second is the name of the directory the repository will be cloned as. The third is the 
location of the repository itself. The fourth is as read/write, this should only be set to write if you have write 
access to the repository. This simply tells the shell to skip this repos when running a push or a status command.

````
/,app,git@github.com:parbake/parbake.git,write
````

An element in the repos array is a comma separated string containing 4 elements. The first is the directory in to 
which


Once you have configured the system be sure to make the parbake file executable
````
chmod +x parbake #as root or sudo
````

Call the parbake shell with a single argument (For the sake of argument I'm calling it a command).
````
./parbake {COMMAND}
````

There are 4 commands with which to call the parbake shell.
*install
*pull
*status
*push

If you are familiar with git you probably have a good idea what these commands do. 

### Install

The install command with remove the existing app directory and build install a fresh copy from the master branch of 
each repository listed in the REPOS array.

### Pull

The pull command will pull the latest updates from the master branch of each repository listed in the REPOS array.

### Status 

The status command run a status check against your local code in case you have forgotten to commit something.

### Push

The push command will push all of your commits to each repository listed in the REPOS array, assuming you have write 
access to that repository.








