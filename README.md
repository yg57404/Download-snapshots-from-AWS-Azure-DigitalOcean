# Download-snapshots-from-AWS-Azure-DigitalOcean
Download snapshots from AWS, Azure, DigitalOcean


AWS, Azure, DigitalOcean is charging for storing images, it's a good time as ever to take things into your own hands and download snapshots to your own PC. To do that, you are going to make a copy of the image's hard drive and save it to a local machine. For the purposes of this article I'm going to copy my old Ubuntu server running Wordpress and MySQL.

First off, login console and Connect via SSH to test if it's working. Now you can start copying the server's hard drive to your HDD. For this we'll use a tool called dd. If you're on Linux, you're good to go; if you're on Windows, then you'll need MinGW or something similar to run dd.

Now run on your machine (source):

    ssh root@ipaddress "dd if=/dev/vda1 | gzip -1 -" | dd of=image.gz

Here "root" is the root-user, "ipaddress" is the IP address of the machine you recently created, "/dev/vda1" is the name of hard drive that you intend to copy (run "df -h" on remote to find the actual name) and "image" is the name of resulting raw image. You might need to add "-p1234" if you changed the default port like I originally did, where "1234" is the alternative port.

The reason for using root here is that by default you are not allowed to use dd as a non-root user. One way to fix this this is to use sudo; I personally went with the less safe way of allowing myself to connect as root via SSH, since on one hand I had Fail2Ban already up and running, and on the other this will be deleted in less than 2 hours.

After running that command you will be prompted to enter your root password. Note that there will be no progress indication after that and in about 10-15 minutes (for the 20GB HDD that is about 10% full) you'll see something like:

41943040+0 records in

Which means you're good to go! After that you have several options:

    Convert the raw image to something suitable for VirtualBox
    Explore the image with help from DiskInternals Linux Reader
Now you can safely destroy the machine. No more wasted money.
