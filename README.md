To automatically mount an SMB share at startup on Ubuntu, follow these steps:

### Step 1: Install CIFS Utilities

First, ensure that the `cifs-utils` package is installed. Open a terminal and run:

```bash
sudo apt update
sudo apt install cifs-utils
```

### Step 2: Create a Mount Point

Create a directory where the SMB share will be mounted. For example:

```bash
sudo mkdir /mnt/mySMBDisc
```

### Step 3: Create a Credentials File

To securely store your SMB credentials, create a file in your home directory:

```bash
touch ~/.smbcredentials
```

Edit this file to include your username and password:

```bash
nano ~/.smbcredentials
```

Add the following lines, replacing `smb_username` and `smb_password` with your actual SMB credentials:

```
username=smb_username
password=smb_password
```

Set the permissions on this file to protect your credentials:

```bash
chmod 600 ~/.smbcredentials
```

### Step 4: Edit the fstab File

Open the `/etc/fstab` file to add an entry for your SMB share:

```bash
sudo nano /etc/fstab
```

Add the following line at the end of the file, modifying it to reflect your SMB share location and mount point:

```
//myWindowsServer.local/SMB-ShareName /mnt/mySMBDisc cifs credentials=/home/yourusername/.smbcredentials,uid=1000,gid=1000,iocharset=utf8,vers=3.1.1 0 0
```

Replace `myWindowsServer.local/SMB-ShareName` with your server's address and share name, and adjust the path to your credentials file as necessary.

### Step 5: Test the Configuration

To test if the configuration works without rebooting, run:

```bash
sudo mount -a
```

This command attempts to mount all filesystems defined in `/etc/fstab`. If there are no errors, your SMB share should now be mounted at `/mnt/mySMBDisc`.

### Additional Notes

- Ensure that the network connection is available at startup, as the SMB share requires it to mount properly.
- If you encounter issues, check the permissions of the mount point and the credentials file, and verify the SMB server's accessibility.

By following these steps, your SMB share will automatically mount at system startup on Ubuntu[1][2][3][5][7].

Citations:
[1] https://gilles.ecgs.lu/mount-smb-shares-automatically-on-linux/
[2] https://community.netcup.com/en/tutorials/setup-smb-autoconnect
[3] https://sahlitech.com/mounting-samba-smb-share-on-ubuntu/
[4] https://www.youtube.com/watch?v=7ni5fq4ozoM
[5] https://ubuntu.com/server/docs/how-to-mount-cifs-shares-permanently
[6] https://obie.hashnode.dev/ubuntu-server-permanently-mounting-samba-shares
[7] https://linuxconfig.org/how-to-mount-a-samba-shared-directory-at-boot
[8] https://askubuntu.com/questions/157128/proper-fstab-entry-to-mount-a-samba-share-on-boot
