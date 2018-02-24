stad-encryption
===============

With STAD-encryption (Secure and Transparant Arbitrary Directory Encryption) you can
easily use LUKS to encrypt only a specific folder and mount it only when necessary.
When the data is not used, one can simply unmount the LUKS-encrypted image to be sure
that the data cannot be accessed by unauthorized users or programs. It also enables users
who don't want to encrypt their whole computer or home directory to encrypt just a
specific folder.

Q&A
---

Q: Why would you use this instead of just using LUKS?
A: Sometimes you need more flexible encrypted directories, and/or making a new partition
for LUKS-encrypted data is not the ideal solution. Furthermore, STAD is made for files
which aren't always in use by the system. When they're not used, you can simple close
the STAD folder to make sure that no other process can read it. Full disk encryption
using LUKS only provides offline protection; once the system is running all data is
accessible.

Q: Is it secure?
A: STAD should be just as secure as any other LUKS-encrypted volume. Be sure to use a
strong and unique passphrase.

How it works
------------

STAD is a toolkit consisting of several neat bash scripts. It is based on LUKS encrypted
image files.

For example, we want to encrypt the folder `~/secret/`.
```
stad-init -d ~/secret -s 1G [-t fstype]
```
While the script runs, it asks us to entry an encryption passphrase by cryptsetup. This
creates a 1GiB ~/.secret.stad file; this is the image where your data is actually stored,
so be sure to back it up!

To open the folder, we run:
```
stad-open ~/.secret.stad
```
Which will prompt us for our passphrase and mounts our directory on `~/secret`.

Once we're done with our secret data, we close it like this:
```
stad-close ~/secret
```

License
-------

```
Copyright (c) 2018 Martijn

stad-encryption is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

stad-encryption is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with stad-encryption.  If not, see <http://www.gnu.org/licenses/>.
```
