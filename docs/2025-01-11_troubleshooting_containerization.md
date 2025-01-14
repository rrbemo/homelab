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

The next step is to try and learn what the standardized way is to pass credentials into a container without making them
visible to anyone who sees or uses the built container.

## Things I need to learn

- View "logs" in podman CLI
- Pass credentials and secrets to containers
  - More generally, I want to know how to build secure containers
    - https://www.youtube.com/watch?v=pHtTqm7M79U (mostly shrinking dependencies, but good stuff)
- 