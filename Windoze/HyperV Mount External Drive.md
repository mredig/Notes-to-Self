<!-- permalink: 61320fa48b7346eea1eaf5dad543a492 DO NOT DELETE OR EDIT THIS LINE -->
# Mount External Drive on HyperV

1. *Manage Computer* on HyperV host
1. Go to *Disk Management*
1. Take the drive you want to connect offline
1. Go to *Settings* on the HyperV VM you want to mount the drive in
1. Go to the *SCSI Controller* hardware entry
1. Add a new *Hard Drive*
1. In the new entry, set the *Physical hard disk* to the disk you took offline
1. In the **VM**, go to *Manage Computer* and *Disk Management* to take the drive back online
1. Once done, in the **VM**, take the drive back offline, remove the device from the HyperV settings
1. The drive should be safe to remove, I think
