# Lab 7

1. Using the useradd command, add accounts for the following users in your system: user1, user2, user3, user4, user5, user6 and user7. Remember to give each user a password.

```bash
sudo useradd user1
sudo passwd user1
sudo useradd user2
sudo passwd user2
sudo useradd user3
sudo passwd user3
sudo useradd user4
sudo passwd user4
sudo useradd user5
sudo passwd user5
sudo useradd user6
sudo passwd user6
sudo useradd user7
sudo passwd user7
```

---

2. Using the groupadd command, add the following groups to your system.

Group                          GID

sales                             10000

hr                                 10001

web                             10002

Why should you set GID in this manner instead of allowing the system to set the GID by default?

```bash
sudo groupadd -g 10000 sales
sudo groupadd -g 10001 hr
sudo groupadd -g 10002 web
```

**Setting GIDs manually ensures unique identification and avoids potential conflicts with system-assigned GIDs.**

---

3. Using the usermod command to add user1 and user2 to the sales secondary group, user3 and user4 to the hr secondary group. User5 and user6 to web secondary group. And add user7 to all secondary groups.

```bash
sudo usermod -a -G sales user1
sudo usermod -a -G sales user2
sudo usermod -a -G hr user3
sudo usermod -a -G hr user4
sudo usermod -a -G web user5
sudo usermod -a -G web user6
sudo usermod -a -G sales user7
sudo usermod -a -G hr user7
sudo usermod -a -G web user7
```

---

4. Login as each user and use id command to verify that they are in the appropriate groups. How else might you verify this information?

```bash
Method 1 : 
- log in as each user.
- use the (id) command to displays the user and group information for the current user.

Mehthod 2:
- without logging in as each user , use the (cat /etc/group) to show the list of groups and the members of each group.
```

---

5. Create a directory called /depts with a sales, hr, and web directory within the /depts

```bash
sudo mkdir /depts
sudo mkdir /depts/sales
sudo mkdir /depts/hr
sudo mkdir /depts/web
```

---

6. Using the chgrp command, set the group ownership of each directory to the group with the matching name

```bash
sudo chgrp hr /depts/hr/
sudo chgrp sales /depts/sales/
sudo chgrp web /depts/web/
```

---

7. Set the permissions on the /depts directory to 755, and each subdirectory to 770

```bash
sudo chmod 755 /depts
sudo chmod 770 /depts/*
```

---

8. Set the set-gid bit on each departmental directory

```bash
sudo chmod g+s /depts/*
```

---

9. Use the su command to switch to the user2 account and attempt the following commands:

- touch /depts/sales/user2.txt
- touch /depts/hr/ user2.txt
- touch /depts/web/ user2.txt

Which of these commands succeeded and which failed? What is the group ownership of the files that were created?

```bash
- The first one only because user2 is in the group that owns the sales directory
- sales group because of the set-gid
```

---

10. Configure sudoers file to allow user3 and user4 to use /bin/mount and /bin/umount commands, while allowing user5 only to use fdisk command.

```bash
#Allow user 3 and user4 to use /bin/mount and /bin/umount
user3 ALL=(ALL) /bin/mount, /bin/umount
user4 ALL=(ALL) /bin/mount, /bin/umount
user5 ALL=(ALL) /sbin/fdisk
```

---

11. Login by user3 and try to unmount /boot.

```bash
sudo umount / boot
```

---

12. Login by user4 and remount /boot. Also try to view the partition table using fdisk.

```bash
sudo mount /boot
sudo fdisk -l /dev/vda
```

---

13. Create a directory with permissions rwxrwx---, grant a second group (sales) r-x permissions

```bash
setfacl -m g:sales:rx dirl
```

---

14. create a file on that directory and grant read and write to a second group (sales)

```bash
setfacl -m g:sales:rw dirl/filel
```

---

15. set the the owning group as the owning group of any newly created file in that directory.

```bash
sudo chmod g+S dirl
```

---

16. Grand your colleagues a collective directory called /opt/research, where they can store generated research results. Only members of group profs and grads should be able to create new files in the directory, and new file should have the following properties:

- the directory should be owned by root
- new files should be group owned by group grads
- group profs should automatically have read/write access to new files
- group interns should automatically have read only access to new files
- other users should not be able to access the directory and its contents at all.

```bash
sudo mkdir /opt/research
sudo chgrp grads / opt/research
sudo chmod g=rwxs /opt/research
sudo setfacl -m d:g:profs:rw /opt/research
sudo setfacl -m d:g:interns:r / opt/research
sudo chmod o= /opt/research
```

---

17. Change your default SELinux mode to permissive and reboot.

```bash
sudo vi /etc/selinux/config
SELINUX=permissive
reboot
```

---

18. After reboot, verify the system is in permissive mode.

```bash
sestatus
```

---

19. Change the default SELinux mode to enforcing.

```bash
sudo vi /etc/selinux/config
SELINUX=enforcing
reboot
sestatus
```

---

20. Change the current SELinux mode to enforcing.

```bash
sudo setenfoce enforcing
```

---

21. Copy /etc/resolv.conf file to root's home directory.

```bash
cp /etc/resolv.conf /root
```

---

22. Observe the SELinux context of the intial /etc/resolv.conf

```bash
ls -Z /root/resolv.conf
```

---

23. Move resolv.conf from root's home directory to /etc/resolv.conf

```bash
mv /root/resolv.conf /etc/resolv.conf
```

---

24. Observe the SELinux of the newly copied /etc/resolv.conf

```bash
ls -Z /etc/resolv.conf
```

---

25. Restore the SELinux context of the newly positioned /etc/resolv.conf

```bash
restorecon /etc/resolv.conf
```

---

26. Observe the SELinux context of the restored /etc/resolv.conf

```bash
ls -Z /etc/resolv.conf
```

---

27. Configure OpenSSH to allow pulic key-based login credentials

```bash
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.original
sudo vi /etc/ssh/sshd_config
PubkeyAuthentication yes
```

---

28. Create an SSH key-pair

```bash
ssh-keygen -t rsa
```

---

29. Configure to login without the need of a password.

```bash
ssh-copy-id mohamedali@localhost
```

---

30. Configure SSH to prevent root logins.

```bash
sudo vi /etc/ssh/sshd_config
PermitRootLogin no
```

---

31. Configure logrotate default setting to compress log files when they are rotated.

```bash
sudo vim /etc/logrotate.conf
```