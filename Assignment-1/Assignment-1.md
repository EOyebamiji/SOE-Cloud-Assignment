## AltSchool SOE-Cloud Assignment

### Create a group "AltSchool"
```bash
sudo addgroup "GroupName"
```
![Created-Group](/AltSchool/SOE-Cloud-Assignment/Assignment-1/assets/addgroup%20altschool.png)

### Create a user, add the user to the created group and set the user to expire after two (2) weeks.
```bash
sudo useradd -e $(date -d "+2 weeks" +%Y-%m-%d) -c "(Optional) Prefered comment" -m -G altschool -p '' "UserName"
```
![Creat-User](/AltSchool/SOE-Cloud-Assignment/Assignment-1/assets/create-user-validity.png)

### Modify the created user to change password on login.
```bash
sudo chage -d 0 "UserName"
```
![Creat-User](/AltSchool/SOE-Cloud-Assignment/Assignment-1/assets/User-password.png)

### Confirm/Verify the set validity of the created user.
```bash
sudo chage -l "UserName"
```
![Creat-User](/AltSchool/SOE-Cloud-Assignment/Assignment-1/assets/User-EOyebamiji-Validity.png)

### Edit the permissions of the group "AltSchool"
Modify the permissions of the group "AltSchool"
```bash
sudo visudo
```
![Modify-Group](/AltSchool/SOE-Cloud-Assignment/Assignment-1/assets/mod-group.png)
Modify the configuration of the group "AltSchool" with the below permissions
```bash
%altschool ALL=(ALL) /bin/cat /etc/*
```
![Create-User](/AltSchool/SOE-Cloud-Assignment/Assignment-1/assets/Sudoers.png)

### Create a new user with no home directory
```bash
sudo useradd -M "NewUser"
```
![Create-NewUser](/AltSchool/SOE-Cloud-Assignment/Assignment-1/assets/User-Create-Oyebamiji.png)

### Confirm the new user does not have the home directory

```bash
ls -l /home/"NewUser"
```
![Create-NewUser](/AltSchool/SOE-Cloud-Assignment/Assignment-1/assets/User-Create-Oyebamiji.png)

![Create-NewUser](/AltSchool/SOE-Cloud-Assignment/Assignment-1/assets/User-Oyebamiji.png)