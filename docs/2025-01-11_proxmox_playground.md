# Proxmox Playground
## 2025-01-11

Since there is a lot of messing around that needs to happen to get kubernetes and containers to work correct, I think
it would be better to use versions of operating systems on proxmox. I've already setup proxmox before, but I'm going to
give it a second round to understand it a bit better. 

Both times I followed Learn Linux TV youtube channel.
- https://www.youtube.com/watch?v=5j0Zb6x_hOk

## Install proxmox

You can download the ISO from proxmox website and install it to a USB via Rufus. After that, install as you would almost
any other usb installer. Below are a few specific settings I made

- Target hard drive: 1.8TB nvme drive (had to select dropdown and change it)
- Password: my super secret password
- Name: proxnasty.local
- IP Address: 192.168.68.220 (this was already a static IP given from my router)
- Gateway: 192.168.68.1 (auto detected)
- DNS: 192.168.68.209 (auto detected)

## Logging in

Once the machine is running and has an IP address, it should show on the display when booted after the install. At this
point there is no need to use the machine hooked up to the keyboard, mouse, and monitor. So long as it has a static IP,
you should be able to login from another computer with the given IP and port. For me, that is currently:

  https://192.168.68.220:8006/
  
Once the page loads it will ask for a login. The login uses the username of "root" and the password you gave it during
the install. 

## Upgrade

The first thing we should do is upgrade the machine and change a few of the repos proxmox checks. First lets assign the
repositories we want:

1. Click on the node (this is "proxnasty" for me)
2. Click on Updates > Repositories
3. Click the Add button
4. Select "no-subscription" from the dropdown and continue
5. Additionally, both of the "enterprise" repositories can be "disabled"

Now lets update:

1. One step up from Updates > Repositories is "Updates", click on that
2. Click the "Refresh" button
3. Wait for the checks to happen
4. Close the window
5. Click the ">_ Upgrade" button
6. Agree to the upgrade if asked
7. Once the upgrade is done, close the window

## Add ISOs

To create a VM, we need to have a boot "drive" available to use. This is usually a ISO. To add ISOs to proxmox:

1. Select the local storage "local (proxnasty)"
2. Select ISO Images from the list
3. Find the location of the ISO you want to upload

## Create Virtual Machine

Creating a virtual machine is a bit more system wide. The button for creating a VM is at the top of the web interface.
You will need to go through many sections/tabs to configure the VM.

1. At the top of the page, click the "Create VM" button
2. Select the Node and give the VM a name and click Next
3. Select the storage and ISO image you want to use to boot/install on the VM, click Next
4. It is common practice to turn on Qemu Agent if possible, so do that and then click Next
5. Update any disk sizeing needs, 32GB is fine for me, and if using SSD, the Discard option was recommended, click Next
6. Changed the core number to what you'd like (in my case I selected 4), keep it under physical count, click Next
7. Change the Memory to what you would like to use ( >= 2GB is recommended), click Next
8. I left network as is, click Next
9. Then review and click Finish

The VM should now be ready to start and install.

## Starting a VM

In the Server View, there should now be a numbered virtual machine. Something like "100 (my-vm-name)". To start the VM,
right click on the VM and select Start. To view a machine, click on the ">_ Console" section (from right click or the 
list that appears whn the VM is selected).

I installed Ubuntu Desktop by just quickly running through the install, as you would on a normal machine. Once the 
install is finished, the VM will likely need to reboot and then you are ready to use it as is. When restarting, you will
need to eject the boot drive. 

### Eject boot media

To do this, go to the Hardware section in the VM list. There should be a iso installed in
the CD/DVD drive. Double-click on the iso name. You should get a popup that you can select an option to not use have 
media installed in the drive.

## Next steps

At this point I have a Ubuntu Desktop machine set up and ready to play around with containers. My next goal is going to 
be experimentation with containers. Eventually I want to move into k3s before setting it back up on bare metal hardware.




















