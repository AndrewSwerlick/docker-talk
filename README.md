Overview
---------

This is a sample project developed for a talk on docker and ansible integration.

It demonstrates how to use docker and ansible to setup an nginx reverse proxy that
can forward requests on to multiple docker containers depending on the host machine

The project consists of a vagrant box, provisioned by a series of ansible scripts.
The box runs docker and two sample rails apps behind an nginx proxy.

This repo also includes the slides from the talk


Dependencies and setup
----------------------
To use the project you have to do two setups steps

1. Install [vagrant](https://www.vagrantup.com/)
2. Add the following lines to your hosts file


    127.0.0.1       bar.localhost
    127.0.0.1       foo.localhost

Running
-------
Run

    vagrant up

to start the vagrant server. This will kick off the ansible provisioning process.
Note the first time you do this is may take a while to run. Depending on your
internet connection it could take over an hour for that first run.

Once the box is provisioned you can browse to bar.localhost:8080 or foo.localhost:8080 to see the results
