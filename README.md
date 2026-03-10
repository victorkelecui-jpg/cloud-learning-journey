# cloud-learning-journey
My cloud journey
# System Files & Configuration
The /etc/ directory is the "brain" of the Linux system.

/etc/passwd: Stores global user account information.

/etc/default/useradd: Contains global default values for new user accounts.

/etc/skel/: Contains skeleton files (hidden configs like .bashrc) copied to new user home directories.

# Essential User Management
When creating users, follow this workflow to ensure a proper environment:

#  Creating a Clean User
# Create user with a home directory and the bash shell
sudo useradd -m -s /bin/bash username

# Set the password
sudo passwd username

# Managing User Environments
Switching Users: Always use the "dash" flag to load the user's environment: su - <username>.

Verifying Setup: Use ls -la /home/<username>/ to confirm hidden configuration files exist. If total 0 appears, the home directory is empty and needs to be repopulated from /etc/skel.

# Advanced Account Security
To manage user access effectively, utilize "chage" and "usermod":

chage: chage is a powerful administrative utility used to change user password expiry information. Think of it as your "security clock" for managing how long a password lasts and when an account should be disable
How to use it: A Quick ReferenceActionCommandCheck 
Current Statussudo chage -l <username>
Force Password Reset on Next Login sudo chage -d 0 <username>
Rotate Password every 30 Days sudo chage -M 30 <username>
Set 7-Day Warning sudo chage -W 7 <username>

Account Expiration
Set Account Expiry: sudo usermod -e 2026-04-10 <username>

Set Password Rotation: sudo chage -M 30 -W 7 <username>

-M: Maximum days before password change is forced.

-W: Warning days before expiration.

Troubleshooting
Permission Denied: Most /etc/ files are restricted. Use cat, less, or vim to view them rather than attempting to execute them.

Cleaning Up: If a user creation fails, ensure you remove the leftover home directory before trying again: sudo rm -rf /home/<username>.

Next Step
You've built a solid foundation here! Since you just updated your system defaults using sudo useradd -D -s /bin/bash, every user you create from here on out will automatically get the bash shell.
