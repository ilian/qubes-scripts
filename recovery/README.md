Recovery scripts
=====
These scripts can be used to recover data from your VMs in the event that your
Qubes OS installation is unable to boot properly.

Rescue
-----
To rescue data, spawn a recovery shell from a Linux installation with the
`dm_crypt` kernel module and the `cryptsetup` tool such as the Qubes OS 
installer. Mount the encrypted partition which contains the data to recover:
```
$ cryptsetup luksOpen qubes
```
The `qubes_dom0` volume group and its volumes should be recognized:
```
$ vgs
$ lvs
```
Mount an external drive to `/mnt/usb` and run the [rescue](rescue) script.

Restore
-----
On a working Qubes OS installation, mount the drive that contain your recovered
data and mount it to `/mnt/usb`. For each VM you want to restore, you will need
to
* Create a new Qube
* Increase its maximum private storage size to at least the size of the restored
data you want to import
* Start and stop the Qube to initialize its filesystem

Run the [restore](restore) script to import the recovered data into the newly
created Qubes. If you do not want to restore a particular VM, press the return
key when prompted for the target VM to restore the data to.

