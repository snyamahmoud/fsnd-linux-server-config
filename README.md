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

4a. SSH public key login for user 'grader'

This is only listed in the rubric, not in the project details.

You will be asked to disable root login by only allowing ssh login to 
non-root users. Also, ssh login should only be possible with ssh public keys, 
password authentication should be disabled. 

This is a very common security best practice: attackers know that every system 
has a user 'root' and will try to login with that account. Attackers do not 
know how you named your non-root users. If password login is enabled and no
further measures taken, an attacker can try to guess the password indefinitely
and may eventually get access that way.

Google terms: 'ssh key authentication'

You can either create a new key pair for the 'grader' user, or just use the
private key that has already been created and configured for the root user.

You will be asked to hand over the private key for that key pair when you
submit the project, so don't use a key pair that you actually use in real life.

Take care that the file permissions on all ssh-related files are set correctly
(it will complain). While you are playing around with SSH keys (and later,
configuration), make sure you ALWAYS stay logged in in at least one shell
window. Do NOT log out until you have successfully logged in with the new
configuration / user / key, or you might lock yourself out of the system.



