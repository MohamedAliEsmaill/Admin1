# Lab 6

## **Using yum**

17. Attempt to run the command gnuplot. You should find that it is not installed.

```bash
gnuplot
```

---

18. Search for the plotting packages.

```bash
yum search plot
```

---

19. Find out more information about the gunuplot package.

```bash
yum info gnuplot
```

---

20. Install the gnuplot package.

```bash
sudo yum install gnuplot -y
```

---

21. Attempt to remove the gnuplot package, but say no

How many packages would be removed

```bash
sudo yum remove gnuplot
```

### **1 package**

---

21. Attempt to remove the gunplot-common package but say no

How many packages would be removed Using rpm

```bash
sudo rpm remove gnuplot
```

### **1 package**

---

22. List all installed packages in your system.

```bash
sudo yum list installed
```

---

23. View the files in the initscripts package

```bash
sudo rpm -ql
```

---

24. Get general information about bash rpm.

```bash
sudo rpm -ql bash
```

---

25. Have the files from the pam package changed since it was installed.

```bash
rpm -V pam
```

---

26. Which installed packages have gnome in their names?

```bash
sudo rpm -qa I | grep "gnomes"
```

---

27. Install any uninstalled package from RH Enterprise Linux cds

```bash
sudo yum install vim
```

---

28. Search for software resemble the Photoshop software other than Gimp and install it.

```bash
yum search image editor | grep —v gimp
sudo yum install drawing.noarch
```

---

29. Create the file /etc/yum.repos.d/cdrom.repo to enable install from the iso from the iso of Red Hat.

```bash
sudo vi /etc/yum.repos.d/cdrom.repo
```

---

30. Try to install any package from the new repository

```bash
sudo yum install vim --repo=DVD-RHEL9-Repository
```