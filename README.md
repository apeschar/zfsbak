# zfsbak

Incremental, compressed and encrypted backups on ZFS.

zfsbak automatically creates a full backup every thirty days. Incremental
backups are based on the last full backup, so that a maximum of two files are
used when restoring.

Backups are compressed using zlib (via `pigz`) and encrypted using GnuPG.

## Set up

Make sure you have the dependencies:

~~~
dnf install -y pigz pv gnupg2
~~~

[Set up GnuPG](https://www.gnupg.org/gph/en/manual/c14.html) so that you have a
public key which with to encrypt your backups. Verify that it works:

~~~
echo Hello | gpg2 -e -r recipient@example.com --armor
~~~

You need a remote server, accessible over SSH, that will store your backups.

## Usage

~~~
zfsbak -r recipient@example.com -h user@host.net tank/home
~~~
