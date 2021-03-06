## Using the VM generated by this project

Download a beta version of the VM:

    ftp://ftp.eu.metabrainz.org/pub/musicbrainz-vm/

Please note that we currently only support VirtualBox. We cannot help with other
virtualization software. The VM will run on any system that VirtualBox supports.

## Logging in

By default the VM will create a private network and be assigned the IP address 10.2.2.2 . In 
order to log into the machine with SSH, do this from the host machine:

    $ ssh 10.2.2.2

Log in with username "vagrant" and password "vagrant". 

## Creating search indexes

In order to use the search functions of the web site/API you will need to build search indexes. Run:

     $ bin/reindex

This process will also take several hours -- be patient. Perhaps it is best to run this overnight.
Please don't complain to us about how long this takes.

## Using the VM 

Once the machine is fully set up, you can connect to the MusicBrainz VM by going to:

     http://localhost:5000

The search service is running on port 8080 if you want to connect to it directly.


## Replication / Live Data Feed

There are a few scripts to make running the VM a little easier. 

Use the set-token script to set the replication token to access the Live Data Feed. There
is no need for you to manually edit the DBDefs.pm file! The set-token script will configure 
the VM with a replication access token you generate from the MetaBrainz site:

     https://metabrainz.org/supporters/account-type

After you've generated the access token, run this:

     $ bin/set-token <replication token>

Then, to replicate the data immediately, you can run:

     $ bin/replicate now

To replicate the data automatically once an hour, you can run:

     $ bin/replicate start

To stop automatic replication, use:

     $ bin/replicate stop


## Troubleshooting

If you get a mysterious error about containers not being started or some-such, try running this command:

     $ vagrant ssh -- bin/reset-containers

Then try the command again that failed.


## Bugs

If any of the scripts above do not work, please tell us what you have done, what you
were trying to do and the output of:

     $ docker ps
     $ docker-compose -f /home/vagrant/musicbrainz/musicbrainz-docker/docker-compose.yml

to 

     http://tickets.musicbrainz.org/secure/CreateIssue!default.jspa

Submit the issue to the "MusicBrainz Virtual Machines" (MBVM) project.
