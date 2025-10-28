<img width="400" height="450" alt="image" src="https://github.com/user-attachments/assets/3e061cb2-20e3-4733-9ce1-7657fe69a7e4" />

# Linux Access Control Management System

## Project Overview
This project demonstrates the implementation and management of access control policies in a Linux environment, focusing on user authentication, group management, and file system permissions. The lab showcases essential cybersecurity practices for maintaining system integrity, confidentiality, and availability of resources.

## 🎯Lab Objectives

This lab demonstrates how to manage access control policies in a Linux machine. First, we will create local user accounts and groups on the system. Then, we will create directories and files where access control policies will be implemented. Further, we will configure the ownership to these directories and files.

## 📋 Project Scenario

Organizations require strict access control mechanisms to protect sensitive data and maintain operational security. This project simulates a corporate environment where:
- Admin Team: Requires full control over security-related projects
- Regular Team: Needs collaborative access to team projects with limited external visibility
- Security Requirement: Prevent unauthorized access while enabling necessary collaboration
----
1- First, we will create two sample users and two groups on this machine and also configure passwords for the two users.

2- In the Terminal window, type sudo su and press Enter to run the programs as a root user

3- In the `[sudo] password for bob` field, type `user@123` as a password and press `Enter`.

4- Type  `useradd testuser01` and press  `Enter ` to create a new user.

5- Type `passwd testuser01` and press `Enter` to set password for the user (`testuser01`).

6- A `New password` field appears, type `test@123` and `Enter`. In the `Retype new password` field, enter the same password (`test@123`) and press `Enter` to set the password. A message appears stating that the `password updated successfully`.

7- Similarly, perform `steps#7-9` to create another user account with username `testuser02` and password `test@123`.

8- Now, create a new group, to do so, type `groupadd admin` and press `Enter`.

9- Similarly, create another group named `team` by issuing command `groupadd team`.

10- In the terminal window, type `usermod -aG admin testuser01` and press `Enter` to add user `testuser01` to the group `admin`.
usermod command is used to modify the user object in order to add a user to the group.

11- Similarly, type `usermod -aG team testuser02` and press `Enter` to add user `testuser02` to the group `team`.

12- Type `id testuser01` and press `Enter` to verify that the user `testuser01` is added to the group `admin`.

13- Similarly, type `id testuser02` and press `Enter` to verify that the user `testuser02` is added to the group `team`.

<img width="700" height="683" alt="image" src="https://github.com/user-attachments/assets/3dd2124d-be24-4c73-af74-8cd2ed0c6a0f" />

-----
14- Now, we will create directories and files to demonstrate how the permissions are applied to them.

15- Execute the commands below to create three directories:
- mkdir testdirectory
- mkdir testdirectory/SecProjects
- mkdir testdirectory/TeamProjects

16- Now, execute the commands below to create two files:
- touch testdirectory/SecProjects/networkreport.txt
- touch testdirectory/TeamProjects/workreport.txt

17- By default, the creator of the directories or resources controls access to the resources. Therefore, users and groups must be permitted to own the directory content which allows them to configure permissions.

18- In the terminal window, type `ls -ld testdirectory` and press `Enter` to display the permissions of `testdirectory` directory.

19- Here, root is the owner of the `testdirectory`

20- Now, we will execute the commands below to change the directory ownership to specfic users and groups:
- The `'R'` parameter allows you to change directory ownership recursively
- `chown -R testuser01:admin testdirectory/SecProjects`
- `chown -R testuser02:team testdirectory/TeamProjects`

21- Type Type `ls -ld testdirectory/TeamProjects` and press `Enter` to display users and groups associated with `testdirectory/TeamProjects`.

22- Type `ls -ld testdirectory/TeamProjects` and press `Enter` to display users and groups associated with `testdirectory/TeamProjects`.

<img width="700" height="439" alt="image" src="https://github.com/user-attachments/assets/3042d1e3-6fc8-41ae-a974-ba0a725fecec" />

---
23- Now configure permissions for the directory owners.

24- In the terminal window, type `chmod u=rwx,g=rwx,o-r testdirectory/SecProjects` and press `Enter` to set the permission below for user `testuser01`.

<img width="482" height="71" alt="image" src="https://github.com/user-attachments/assets/4e62eec1-86f1-431b-9ef2-1937d543e01f" />

<img width="700" height="484" alt="image" src="https://github.com/user-attachments/assets/4e4ae39d-8c32-4e20-ae64-38d5a576f6b2" />


`Access Level Parameters: r`: read a file or list a directory's contents, `w`: write to a file or directory, `x`: execute a file or recurse a directory tree.

`Reference Parameters: u`: user (file owner), `g`: group (members of the file's group), `o`: others (users who are neither the file's owner nor members of the file's group).

`rwx`: read, write and execute permissions are given to u(user) and g(group), `o-r`: Read permission is removed for o (others).

-----

25- In the terminal window, type `chmod u=rwx,g=rwx,o=rx testdirectory/TeamProjects` and press `Enter` to set the below permission for user `testuser02`.

<img width="464" height="62" alt="image" src="https://github.com/user-attachments/assets/4518d30b-48e0-4ce8-82f7-3d319766ad51" />
<img width="700" height="471" alt="image" src="https://github.com/user-attachments/assets/6a3654ac-a06d-4e91-9b02-fb65d9f24b97" />

Here, `rwx`: read, write and execute permissions are given to u(user) and g(group), `rx`: Read and execute permissions are given to o(others).

----
26- Now, that we have created the user accounts along with the specified resource access policies, we will test them.

27- Click on `Add` icon (`+`) present on top-left corner of the `Terminal` window to open another terminal.
<img width="700" height="440" alt="image" src="https://github.com/user-attachments/assets/471fcbbd-660b-46e2-b984-d85d79ff5847" />

----
28- A new `Terminal` window appears, in another tab.

29- In this new `Terminal` window, type `su testuser02` and press `Enter`.

`su` stands for substitute user, it is used to execute commands with the privileges of another user account.

30- A `Password` field appears, type `test@123` and press `Enter`.

The password that you type will not be visible.

31- In the terminal, type `cd testdirectory/SecProjects` and press `Enter`, to navigate to the `SecProjects` directory having only `Admin` privileges.

32- Type `ls` and press `Enter` to list the files present in the directory.

33- According to permissions specified in `step#26`, you can observe that the `testuser02` does not have access to the directory content of `testuser01`. The `testeruser02` being a normal user has limited access whereas `testuser01` has admin level privileges.

<img width="800" height="490" alt="image" src="https://github.com/user-attachments/assets/bb8e0cd3-e500-4c6b-be7c-839b0aa9f5eb" />

#As described above, a root user can create multiple useraccounts on the same machine with different level of access permissions, thereby, preventing unauthorized access to the system and resources.

-----
📝 Use Cases
This project is applicable to:
- Corporate IT security implementations
- Multi-user system environments
- Compliance requirements (HIPAA, PCI-DSS, SOX)
- DevOps security practices

