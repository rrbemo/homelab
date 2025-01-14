# Troubleshooting migration to container

I was running into all kinds of problems while trying to containerize race_sim_telemetry. I wasn't sure what the issue
was, but I knew there were some underlying issues which were not allowing certain things to happen. To help debug, I 
decided that I was going to use a Desktop OS to use podman Desktop to see if I could get the container running well. So,
I moved over to using proxmox with Ubuntu Desktop.

In proxmox, I'm running Ubuntu Desktop with an install of podman desktop. I've cloned the race_sim_telemetry git repo,
set up a container using the Containerfile I created and tried to run it. It failed almost instantly. 

## Log

In podman desktop, I was able to troubleshoot easily with the "log" tab. 

### Issue 1

The first issue was that "plotly" was not found during the initial loading. This was easily fixed by adding "plotly" to 
the requirements.txt.

After fixing that I removed the container and re-built it with the UI. I ran it again and, to my suprise, it never 
crashed! However, when I started poking around into the web interface, I found another issue.

### Issue 2

The second issue was that I didn't have the "config" file, which has credentials for a part of the app. In this case, I
was able to use the log tab again to find that there was a "file not found" error. The file was my config file. 

I converted the config file to a .env file and used environment variables for the time being. The password for the 
postgresql database is able to be seen when inspecting the container, but that isn't a big issue at this time. 
Eventually I would like to have it use secrets so that it is not as open.

### Issue 3

The third issue was that the UDP traffic was not reaching the container/application. Nothing was being read when playing 
F1 23 and no postgresql database activity was happening. I susspected that maybe proxmox was stopping traffic. I tried 
a netcat command to see if traffic was comming through. 

    netcat -ul 22023

This showed that something was getting through, although not exactly definitive. So, I decided that UDP traffic was not 
getting to the container. 

To fix this, I added a port mapping designation of host 22023 to container 22023/udp. This seemed to fix the issue. The 
configuration was when starting the image, about half way down the page. In the command line I believe it would look
something like:

    ... -p 22023:22023/udp

I now have the application running basically as good as it was running on my laptop. It was pumping up to 500 
transactions per second to the postgresql database. I believe this is a lot higher rate. Likely due to the fact that all 
traffic is hard wired.

## Next Steps

I'm considering this troubleshooting process complete. The application is running the same, if not better than it was 
before. From this point on, I need to focus on efficiencies of reading and writing the data.

## Things I need to learn

- View "logs" in podman CLI
- Pass credentials and secrets to containers
  - More generally, I want to know how to build secure containers
    - https://www.youtube.com/watch?v=pHtTqm7M79U (mostly shrinking dependencies, but good stuff)
- 