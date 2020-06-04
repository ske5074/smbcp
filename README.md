<B>Samba aware copy command for unix systems using scp like parameters.</B>

smbcp is a wrapper script that calls smbclient to copy a file to/from a Windows cifs share to/from a unix system using scp like parameters.

After dealing with end users of a unix system that needed to regularly move files to and from different Windows systems and determining that a smbmount type solution is to overbearing and admin heavy, I wrote smbcp. If a user knows how to use scp, it's similar so there's not much of a learning curve. It also transfers files without the need to mount the Windows host before hand or perform ftp like commands with smbclient. Many unix flavors come with smbclient so smbcp should be relatively easy to be ported to different unix versions.

I've only tested on Sun Solaris systems but hope to get it portable. The code is also very rough - proof of concept rough even though I have users using it currently. The script smbrm is a hack of smbcp that provides a way for a unix user to delete a file from a windows host. A smbcp command followed by a smbrm command provides a way to emulate the mv command.

smbcp does not currently support multiple file transfers which should be integrated. smbclient doesn't have a easy way to handle multiple files without doing a tar type of operation so there's some work that needs to be done.

Usage:

smbcp {source} {destination}

source|destination = {username}[%password]@{hostname}:{filename} | {filename} The var SMBPASSWD can also be used.

Example:

$ smbcp sean%mywinpasswd@bob:/s\$/hithere/wow.txt ~/wow.txt

To copy multiple local files, this works...

$ for i in txt; do smbcp "${i}" "sean%mywinpasswd@bob:/s$/overthere/${i}" ; done
