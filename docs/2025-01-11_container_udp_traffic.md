# Route UDP traffic to container
## 2025-01-13

I was having issues getting a container to receive UDP packets for race_sim_telemetry sent on my network. 

## Goals

- Container to receive UDP packets on 22023

## Narrow down the issue

I was running a container inside a proxmox VM. I did some troubleshooting using netcat to determine that the VM was able
to receive UDP traffing on 22023.

        netcat -ul 22023

Which led me to believe the issue was podman or the container.

## Mapping ports

In podman desktop, I had to map the 22023 host port to 22023/udp port on the container. I did this through the interface
when running the container. I beieve the argument for cli would be something like this:

        ... -p 22023:22023/udp

Now that the application is able to read UDP traffic and write to the postgresql database, it is time to optimize the 
application.

## Next steps

Next I will work on optimizing the race_sim_telemetry application.