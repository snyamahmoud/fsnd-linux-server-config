## FSND Project 5: Linux Server Config

This is not a copy & paste walkthrough. It still is full of spoilers.

1. The VM

Udacity will provide a virtual machine running in the Amazon cloud. The
IP address is given on your Udacity account page. The VM can be also be
managed (as in: created/started and deleted) from that page.

You will not find the page "Development Environment" in the "My Account"
menu on the left. The link is given in the project details for P5.

2. SSH

On your hidden development environment page you can also download the 
private ssh key to use for login as root to your Amazon instance. To use it,
download the private key, and move it to the .ssh directory in your home.
Make sure the file has the correct permissions, or ssh will refuse to
use it.

Google terms: 'ssh private key location', 'ssh permissions too open'
(These steps are also documented on the development environment page.)

3. Users
You will be asked later to disable direct logins for the root user for 
security reasons. If you do so, you need a different user to login with.
In this project, it is specified that this user should be called 'grader'.

Create this as a standard Linux user.

Google terms: 'ubuntu add user'

If you are bored, find out the difference between the 'adduser' and 'useradd'
commands.

4. Sudo

There are several ways to allow a user to execute commands with sudo. The
'ubuntu way' is using the /etc/sudoers.d/ directory. It is pretty
self-explanatory, but if in doubt:

Google terms: 'ubuntu sudoers.d'

In this step, make sure the 'grader' user can use sudo.
