Postgres
========
Manuals for postgres:  
[Starting the database cluster](http://www.postgresql.org/docs/8.2/static/creating-cluster.html)  
[Starting the database server](http://www.postgresql.org/docs/8.2/static/server-start.html)  

### Run at load and Keep Alive features  
You can enable or disable these features modifiying the file `~/Library/LaunchAgents/homebrew.mxcl.postgresql.plist `. Edit the xml in the file, setting to true/false these properties.

### Create a database cluster  
A database cluster needs to be created. This is a collection of databases that is managed by the database server. When the cluster is created, the _postgres_ database is created. This the default database for use by utilities, users and third party applications. The location for the data files is optional, although there are several popular locations such as `/usr/local/pgsql/data` or `/var/lib/pgsql/data`.  
The command for cluster initialization is:  
`initdb -D /usr/local/var/postgres`  
### Start/Stop Postgres
In order to start postgres, you can run this command in the terminal:  
`postgres -D /usr/local/var/postgres`  
The `pg_ctl` program, is a wraper to simplify postgres syntax.  
`pg_ctl start  -D /usr/local/var/postgres -l logfile` will start postgres in the background and will store logs.  
`pg_ctl` can also stop the database: `pg_ctl stop  -D /usr/local/var/postgres`  
### Setting up data directory
If you want to avoid to type the whole data directory everytime you start/stop your database, you can:  
- add the data directory as a environment variable: add `export PGDATA="/usr/local/var/postgres"` to `~/.bash_profile`. Why on .bash_profile and not on .bashrc?. The anwser is [here](http://www.joshstaiger.org/archives/2005/07/bash_profile_vs.html)

### Foreign Keys - Referential Integrity
You want to make sure that you don't have an entry in a table with an association that doesn't have a correspondent entry in the associated table. For that purpose you can use the foreign keys.
