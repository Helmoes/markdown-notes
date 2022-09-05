A snapshot includes the contents of the virtual machine memory, virtual machine settings, and the state of all the virtual disks. When you revert to a snapshot, you return the memory, settings, and virtual disks of the virtual machine to the state they were in when you took the snapshot.

You might want to take snapshots in a linear process if you plan to make changes in a virtual machine. For example, you can take a snapshot, continue to use the virtual machine from that point, take another snapshot at a later point, and so on. You can revert to the snapshot of a previous known working state of the project if the changes do not work as expected.

If you are testing software, you might want to save multiple snapshots as branches from a single baseline in a process tree. For example, you can take a snapshot before installing different versions of an application to make sure that each installation begins from an identical baseline.

![[GUID-B5FC55DE-79E3-4828-B806-DD80D6206652-high.png|500]]

When you delete files from your virtual machine, the disk space occupied by those files is not immediately returned to your host system. If a virtual disk has such empty space, you can use the Clean up disks command to return that space to the hard drive on a Microsoft Windows host.
You can use the Clean up disks command with virtual machines that have snapshots or are linked clones or parents of a linked clone.