# Migrate config to envs
## 2025-01-13

Migrate my use of config.yaml file as a set of parameters to connect to the postgresql database to using env variables.
This won't be perfect for all values in the yaml, as I use a password, but it will be ok for now.

Environment vars and .env:
- https://nikhilakki.in/handling-environment-variables-in-containers-dockerpodman

Pass environment variables on run, especially .env:
- https://stackoverflow.com/questions/30494050/how-do-i-pass-environment-variables-to-docker-containers

Docker/containerignore. He at least explains it a little.
- https://www.youtube.com/watch?v=SnSH8Ht3MIc

## Goals

- Replace flat file credentials with build options
- Replace code use of flat files in place of environment variables

## Convert code

In race_sim_telemetry, my simstore.py file reads in a config.yaml file. The config.yaml file has a bunch of different 
information about how to connect to the postgresql database.

- user
- password
- host ip
- port
- database name

Before going any further, I need to say that there are a lot of issues with putting secure information in environment 
variables, especially if they are assigned during the build process. There are more secure ways to do this, which I want
to look into later. For now though, this is fine for this use case. 

1. To convert this over to using environment variables, the first thing I had to do was import os to the python file. 

        import os

2. commented out the old cold that pulled in the config file data.
3. wrote new assignments to the values I needed using environment variables.

        usr = os.getenv("RST_PGSQL_USER")
        ...
        db_name = os.getenv("RST_PGSQL_DBNAME")

That shoud just about do it for the code side of things. At his point, I need to replace the file with something else.

## Replace flat file

At this point, I could just add env variables one by one when building or running. Instead, I've decided to use a .env 
file to load when running. This will make sure my specific values are not default if this image is shared after the 
build process. 

The .env file is something like:

        RST_PGSQL_USER=user_name
        ...
        RST_PGSQL_DBNAME=my_db_name

Don't forget to add the .env file to the .gitignore and .containerignore if it is put within the project (I put it in 
ther root directory).

## Build and run

Since code changed, the image needed to be rebuilt. I'm still using podman desktop at this point for troubleshooting, so 
I created a new container and built it with normal settings, not adding any environment variable values.

I then wen to the images section and found the new image. I clicked the play (run) button. In the first options screen
(Basic), there is an option to add "Environment files:". I clicked the browse button and selected the .env file I made 
earlier. I then clicked "Start Container".

The container seemed to run just fine.

## Testing the application

I need to test that the code is at least pulling in the environment values. 

1. I navigated to the local host website, it loaded just fine
2. tried /session site to try and load data, it loaded with data!
3. What!? It just worked!?

Yea, it just worked. I was quite concerned that the VM/container would not be able to access my postgresql db. However, 
it seems to work just fine. I'm a bit concerned that it can access my local network so easily, but I suppose that there
are some proxmox settings to tighten down security.

## Next Steps

I need to test the ingress of UDP packets to my application. That shouldn't be too difficult to test... Time to load of 
F1 23 and race a little :)

### Learn next

- better ways to secure password (podman secrets?)
- networking into the container?