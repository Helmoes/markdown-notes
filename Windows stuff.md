[[PowerShell]]

![[nosync/To-Do#Windows]]

# Hard/soft links
[NTFS Hard Links, Junctions and Symbolic Links](https://www.2brightsparks.com/resources/articles/ntfs-hard-links-junctions-and-symbolic-links.html)
NTFS supports both hard links and soft links, also known as symbolic links. Hard links are supported only for files, while symbolic links can be used with files or directories.

A hard link allows multiple paths to refer to the same file on a single volume. For example, if you create a hard link named C:\Docs\Spec.docx that refers to the existing file C:\Users\Abby\Documents\ Specifications.docx, the two paths link to the same on-disk content and you can make changes to either path. NTFS implements hard links by keeping a reference count on the file data on disk. Each time a hard link is created, NTFS adds a file-name reference to the data. Because the file data is not deleted until the reference count is zero, you can delete the original file (C:\Users\Abby\Documents\ Specifications.docx in our example) and continue to use other hard links (C:\Docs\Spec.docx). The file data shared by hard links includes not only the file’s content and alternate stream data, but also the file’s security descriptor, time stamps, and attributes such as whether the file is read-only, system, hidden, encrypted, or compressed.

By contrast, symbolic links are strings that are interpreted dynamically and can be relative or absolute paths that refer to file or directory locations on any storage device, including ones on a different local volume or even a share on a different system. This means that a symbolic link does not increase the reference count of the original file-system object. Deleting the original object deletes the data and leaves the symbolic link pointing to a nonexistent object. File and directory symbolic links have their own permissions and other attributes, independent of the target file-system object.

You can create hard links, symbolic links, and junctions in Windows Vista and newer with the `mklink` command built into Cmd.exe. [mklink](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/mklink)
```powershell
mklink [[/d] | [/h] | [/j]] <link> <target>
```
- `/d`: Creates a directory symbolic link. By default, this command creates a file symbolic link.
- `<link>`: Specifies the name of the symbolic link being created.
- `<target>`: Specifies the path (relative or absolute) that the new symbolic link refers to.

# Tools
Installed on 5/9/22:
- usbview
- devcon

# Access ext4 partitions from windows
- DiskInternals Linux Reader (chose this one for the moment)
- Linux File Systems for Windows by Paragon Software (also looks good, paid maybe better)
- Ext2explore
- ext2fsd
- 