# homelab

My homelab notes and scripts.

## My current homelab

**Create files for each device in my homelab and link them the specs and what is setup on that device.

- LincStation N1
  - 4x 2TB nvme drives
    - Raid Z1
  - 2x 2TB 2.5" 5400rpm HDD
    - Striped (no redundancey)
  - Truenas
    - Jellyfin
    - Audiobookshelf
- Raspberry pi 4
  - Rasbian?
    - pihole
    - PostgreSQL
- ThinkCentre M920q
  - i5 8500T (6 cores x 6 threads)
  - 16GB 2666Mhz RAM
  - Dual 2.5Gbps PCIe Nic (Realtek)
  - OPNsense router (in progress)
- ThinkCentre M75q Gen2
  - Ryzen 5 PRO 5650GE (6 cores x 12 threads)
  - 32GB 3200Mhz RAM
  - Proxmox
    - VMs only for learning (no production apps)

## Tools of interest

- Proxmox
  - VMs
- containers
  - containerd
  - podman
- kubernetes
  - k3s
  - postgresql
  - model training
  - game server(s) (pteradactyl?)
- Truenas
  - backups
  - ACL best practices
  - other features
- graphana

## Goals

- learn about self-hosted technologies/tools
  - roughly follow a set of Standard Operating Procedures (SOP)
- journal my learning (docs)
- implement *production*, self-hosted tools that I find useful
  - kubernetes
  - websites
  - web applications

### Documentation

The "docs" folder contains markdown files with documentation on what I did. Usually this documentation can be followed 
to replicate what I did, however, it is not meant to be instructions. It is rather a journal of what I wanted to do, 
resources I used, what I did, and what I plan to do next on the topic.

Each markdown should be specific to something I want to lear or ended up learning the the process of completing something
else. The file naming convention is [date started]_[description].md. 

Within the file, I'm roughly using the template of:




    # Title
    ## Date
    
    [description]
    [list of resources (tutorials, documentation, etc.)]

    ## Goals

    [Overall description]
    [list of goals]
    
    ## Tools (sometimes)

    [list of used tools and links]

    ## [Process 1 ...]

    [description]

    ...

    ## Next Steps

    [description of what I plan to do next]

    ### Learn next

    [list of things I want to learn about]



#### Need to learn more

Within the docs folder there is a need_to_learn_more folder. Inside this is a set of documentation which was started but
never finished or was put on hold to learn more. I may pick these back up, but it is likely that once I learn more I 
will end up creating new documentation altogether. 

## *Standard* Operating Procedures

Not really SOPs, but there is a general set of guidelines I want to follow while learning new things. 

1. Start a markdown document when starting something new
   - Keep learning objectives bite-sized (~1 hour or less)
   - If a topic is too large, make a new document for the underlying knowledge needed
2. Use VMs when possible first
   - I want to break my habbit of deploying things directly to bare metal systems
3. Use a fresh VM if possible
   - Running through the creation process should help solidify the learning
   - #TODO: I should probably create a snapshot or something on a fresh install... 
