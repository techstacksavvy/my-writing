![Banner](https://github.com/techstacksavvy/my-writing/blob/creating_new_user_linux/images/Pink%20and%20Blue%20Digital%20Brainstorm%20Presentation.gif)

# Linux User Creation Guide 👩🏾‍💻

# Overview

This guide covers creating a new user on Linux, emphasizing user account importance, permission management, and security. It includes steps for accessing the terminal, using useradd, setting passwords, assigning user groups, configuring home directories, and verifying user creation. Troubleshooting tips and additional resources enhance user management understanding.

## Before you start

This guide assumes that you have basic computer knowledge and limited experience with Linux.

# Table of Contents

- [Overview](#overview)
  - [Before You Start](#before-you-start)
- [Table of Contents](#table-of-contents)
- [Define User Accounts](#define-what-user-accounts-are-in-a-linux-environment)
  - [The Importance of Creating User Accounts](#the-importance-of-creating-new-users)
- [Access the Terminal](#access-the-terminal)
- [User Creation Command](#user-creation-command)
    - [Create New User](#create-a-new-user)
    - [Set Password](#set-passwords)
    - [Assign User to a Group](#assign-user-groups)
    - [Home Directory Configuration](#home-directory-configuration)
    - [Verify User Creation](#verify-user-creation)
    - [User Deactivation](#user-deactivation)
- [Troubleshooting Tips](#troubleshooting-tips)
- [Conclusion](#conclusion)
- [Additional Resources](#additional-resources)


# Define What User Accounts Are in a Linux Environment

Think of user accounts like different keys to unlock parts of a computer. These keys help the computer do things without letting it have full control over everything.
 
In a Linux system, processes fall into two categories: Kernel mode and user mode. Kernel mode tasks, like creating users, editing configuration files, and installing new programs have elevated privileges and unrestricted access to the core functions of the operating system. On the other hand, user mode processes, such as creating a Word document, using the calculator, or browsing the web, run with limited permissions to ensure system security and integrity.

### The Importance of Creating New Users

User accounts are necessary in Linux for several reasons. They are needed to grant the necessary permissions for various tasks, ensuring that individuals can perform their work effectively. 

Additionally, proper user management is crucial to maintaining the security and integrity of the Linux environment. In summary, user accounts facilitate the allocation of permissions, enable people to carry out their tasks, and contribute to the overall security of the system.

# Access the Terminal

The terminal also known as a command line interface(CLI) differs from a graphical user interface(GUI) in that it operates solely based on commands a user inputs in the terminal. The GUI operates via visual elements where you’re able to point and click. 

**Steps to Open Terminal:**

1.  Open the menu by clicking on the "Activities" button in the top-left corner (for GNOME-based desktops) or the menu button in the bottom left (for other desktop environments).

2.  Type "Terminal" in the search bar.

3.  Press Enter or click on the "Terminal" icon in the search results.

![Terminal](https://github.com/techstacksavvy/technical-writing-drafts/blob/creating_new_user_linux/images/terminal.png)

# User Creation Command

The `useradd` command allows the user to add a user account from the command line.

Basic Syntax

```
useradd [options] username
```

## Create a New User

Creating a simple user: 

This command will create a user named Sasha. 

```sudo useradd Sasha```

![New User](https://github.com/techstacksavvy/my-writing/blob/creating_new_user_linux/images/useradd.png)

This command will create a user named Sasha and add him to the accountant group. 

```sudo useradd -G accountant Sasha```

![](https://github.com/techstacksavvy/technical-writing-drafts/blob/creating_new_user_linux/images/usermod_g.png)

> Note: The `sudo` command is utilized here because elevated permissions are required to create a new user. You will be prompted to enter the root user password.
> 
> If you want to create a new group, type the following command, `sudo groupadd groupname`.

If you type the following command in the terminal, `groups Sasha` you will see that Sasha is now a part of the accountant group.

![](https://github.com/techstacksavvy/technical-writing-drafts/blob/creating_new_user_linux/images/accountant_group.png)

## Set Passwords

The `passwd` allows the user to create a password for a user.

Basic Syntax

```
passwd [options] username
```

This command will create a password for the user Sasha. 

```sudo passwd Sasha```

Enter your desired password and then renter it when prompted.

The result should be `passwd: password updated successfully`.

![Password Command](https://github.com/techstacksavvy/technical-writing-drafts/blob/creating_new_user_linux/images/passwd.png)

## Assign User Groups

The `usermod` command is used for modifying user properties, such as adding a user to an additional group.

Basic Syntax

```
usermod [options] username
```

This command will add Sasha to the sales group as a secondary group. 

```sudo usermod -aG sales Sasha```

![Secondary Group](https://github.com/techstacksavvy/technical-writing-drafts/blob/creating_new_user_linux/images/usermod_ag.png)

User groups help you to define a set of permissions that you can then impose on other users.

## Home Directory Configuration

Home Directories serve as the storage space for a user's personal files. For instance, this is where a user can keep documents, photos, and other personal data.

Executing this command will establish a new user account named Diane and generate the associated home directory, which will be located at `/home/Diane`.

```
useradd -m Diane
```
![](https://github.com/techstacksavvy/technical-writing-drafts/blob/creating_new_user_linux/images/useradd_m.png)

## Verify User Creation

The `/etc/passwd` file is a plain text file with information for all user accounts. It includes a list of user accounts on your computer, as well as details such as user ID, group ID, home directory, and default shell. 

To verify the successful creation of the new user enter the following command  
 
```
sudo cat /etc/passwd
```
![](https://github.com/techstacksavvy/technical-writing-drafts/blob/creating_new_user_linux/images/etc_passwd.png)

## User Deactivation

To deactivate or lock and unlock a user account with the passwd command enter the following command: 
 
```
sudo passwd -l username
```
![](https://github.com/techstacksavvy/technical-writing-drafts/blob/creating_new_user_linux/images/passwd_l.png)

```
sudo passwd -u username
```
![](https://github.com/techstacksavvy/technical-writing-drafts/blob/creating_new_user_linux/images/passwd_u.png)

## Troubleshooting Tips

1.  Permissions: Ensure you have the necessary permissions to create users. Use the `sudo` command to execute user-related commands with elevated privileges.

2.  User Already Exists: Check if the username is already in use. Usernames must be unique.

3.  Incomplete Information: Provide all required information when creating a user, such as a password. Some systems may require additional details like the user's full name.

4.  Home Directory Creation: If the home directory is not being created, ensure the `-m` option is used with the `useradd` command.

5.  Group Membership: If you need to add the user to specific groups, use the `usermod` command.

6.  Password Issues: If you encounter password-related problems, ensure you set a password for the user using the `passwd` command.

7.  Check Logs: Examine system logs, such as `/var/log/auth.log` or `/var/log/secure`, for any error messages or clues.

8.  Review Documentation: Refer to the documentation specific to your Linux distribution for any distribution-specific considerations or requirements.

9.  Check System Resources: Ensure there is sufficient disk space and system resources to create a new user.

## Conclusion

This comprehensive guide outlines the process of creating a new user on a Linux operating system, catering to users with basic computer knowledge. It emphasizes the significance of user accounts in managing system permissions and maintaining security. The steps include accessing the terminal, using the useradd command for user creation, setting passwords, assigning user groups, configuring home directories, and verifying user creation through system files. Troubleshooting tips address common issues, and additional resources provide opportunities for users to explore advanced user management features. 

## Additional Resources 

- Linux User Management Best Practices and Tips - https://www.linkedin.com/pulse/linux-user-management-best-practices-tips-ephrem-assefa/

- Official useradd Manual Page - https://man7.org/linux/man-pages/man8/useradd.8.html

- Password Security - https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/4/html/security_guide/s1-wstation-pass
