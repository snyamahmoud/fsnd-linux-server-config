## FSND Project 5: Linux Server Config

This is not a copy & paste walkthrough. It still can be consider

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

  **Google terms: 'ssh private key location', 'ssh permissions too open'**
  (These steps are also documented on the development environment page.)

3. Users

  You will be asked later to disable direct logins for the root user for 
  security reasons. If you do so, you need a different user to login with.
  In this project, it is specified that this user should be called 'grader'.

  Create this as a standard Linux user.

  **Google terms: 'ubuntu add user'**

  (If you are bored, find out the difference between the 'adduser' and 
  'useradd' commands.)

4. Sudo

  There are several ways to allow a user to execute commands with sudo. One
  simple way prepared for you by the Debian/Ubuntu distribution maintainers
  is using the /etc/sudoers.d/ directory. For details:

  **Google terms: 'ubuntu sudoers.d'**

  In this step, make sure the 'grader' user can use sudo.

  1. SSH public key login for user 'grader'

  This is only listed in the rubric, not in the project details.

  You will be asked to disable root login by only allowing ssh login to 
  non-root users. Also, ssh login should only be possible with ssh public 
  keys, password authentication should be disabled. 

  This is a very common security best practice: attackers know that every 
  system has a user 'root' and will try to login with that account. Attackers 
  do not know how you named your non-root users. If password login is enabled 
  and no further measures taken, an attacker can try to guess the password 
  indefinitely and may eventually get access that way.

  **Google terms: 'ssh key authentication'**

  You can either create a new key pair for the 'grader' user, or just use the
  private key that has already been created and configured for the root user.

  You will be asked to hand over the private key for that key pair when you
  submit the project, so don't use a key pair that you actually use in real 
  life.

  Take care that the file permissions on all ssh-related files are set 
  correctly (ssh will complain). While you are playing around with SSH keys 
  (and later, configuration), make sure you ALWAYS stay logged in in at least 
  one shell window. Do NOT log out until you have successfully logged in with 
  the new configuration/user/key, or you might lock yourself out of the 
  system.

5. Update all installed packages

  **Google terms 'ubuntu update packages'**

  Manual update is easy -- don't forget you need use sudo to do this, and
  don't let the different subcommands of apt-get confuse you.

  In the rubric you'll find that for 'exceeds specifications' you need to
  configure automatic unattended package updates. This is a bit controversial,
  as every update also has a chance to break your system due to configuration
  or setup changes you need to implement in your applications to run them on 
  the newer versions of your platform (web server, databases etc.).

  It is, however, possible to only install security updates automatically. 
  This might be a good compromise depending on your needs. Security updates 
  should be installed as soon as possible, and the distributions (usually) 
  don't include dangerous changes or version upgrades in security updates. You   still should subscribe to the security announcement channels of the 
  distribution you are using, and of course monitor the activity of any 
  automatic updates you have set up, e.g. by having your scripts or tools
  send you notification emails.

  **Google terms 'ubuntu automatic security updates'**

6. Use a non-standard port for SSH

  The rationale for this is similar to that for not using the root account
  for login: attackers know that the ssh service is usually listening on port
  22, so they point their attacks there. If ssh is listening elsewhere, they
  at least have to find out where first.

  **Google terms: 'linux sshd use different port'**

  The project asks us to use port 2200. As said above, don't log out of
  your working ssh session before you have confirmed you can log in on the
  new port!

  Also, be sure you understand the difference between 'ssh' and 'sshd' and
  their respective config files.

  1. Disable root ssh login

  This is only listed in the rubric, not in project details: as mentioned
  above, decline any login for the root account through ssh, always. This
  is done in the ssh configuration, look at the corresponding config file
  for hints, or **google 'linux ssh disable root login'**.

7. Firewall

  You can set up your system in a way that it only accepts traffic on
  certain ports and blocks everything else. The traditional linux tool to
  do that is 'iptables'. As this is powerful but hard to use for beginners,
  ubuntu comes with a firewall setup tool that is much easier to use: 'ufw',
  the 'uncomplicated firewall'.

  **Google terms: 'linux firewall setup', 'ubuntu ufw'**

  The project explicitly asks us to use 'ufw', so only spend time on 
  'iptables' documentation if you are curious. It is not needed to configure
  the firewall as requested.

  We are asked to block everything, and allow incoming connections for these
  services:

  - SSH on port 2200 (we moved it there in the step above)
  - HTTP on port 80 (we will run a webserver later)
  - NTP on port 123 (network time protocol, explained in the next step)

  The ubuntu documentation of UFW is detailed enough to do this. You configure
  the firewall by calling

  $ sudo ufw [allow|deny] [service|port]

  Don't forget to enable the firewall when you're finished configuring it. 
  Also, when it is enabled, make sure you can still log in before logging 
  out of your running ssh session! This is another excellent opportunity to
  lock yourself out from your own VM.

  If you are curious where the configuration you entered on the command line
  is stored, **google 'ubuntu ufw rules stored'**. Also remember that the
  'ufw status' command has a 'verbose' option for more information.

  I was wondering why we are asked to open port 123 for ntp: the firewall
  in general allows all connections initiated by a service on the system
  (i.e. 'outgoing'), and ntp runs as a daemon and should be covered by this.

  However, I found a few discussions of this questions when **googling for
  'ntp firewall bidirectional'**, and as it's explicitly written in the
  project details, I've opened the port as well.
  
  1. Monitoring

  For 'exceeds expectations' we are asked to monitor unsuccessful connection
  attempts, block the IP addresses they come from, and send an email
  notification about the fact.

  A good starting point is **googling for 'ubuntu block ip after failed 
  login'**.

  When googling, remember that we are using 'ufw' for firewall configuration
  instead of 'iptables', you might want to refine your search terms.

8. Date and Time

  The project details ask for the system to be running on UTC time.

  **Google terms: 'timezone utc gmt'** for a bit of (historical) background
  about timezones and UTC,

  **Google terms: 'ubuntu set timezone'** for how to do it.

  NTP is a service that requests accurate time from external time servers
  and adjusts the server clock accordingly. It is not specified anywhere that 
  ntp should be set up, but a) you really want the correct time for all sorts
  of reasons (**google 'why ntp is important'**, and b) as we already opened 
  the ntp port in the firewall we can just as well use it.

  **Google terms: 'ubuntu ntp'**

  There are several options, I chose the one where a daemon is always running
  and taking care of the time synchronisation. 

9. Apache Web Server & WSGI

  Apache is a web server implementing the HTTP standard. On its own it
  delivers files from the file system to the user's browser. If there is
  code to be executed, i.e. a full-fledged web application backend running,
  Apache is usually extended with modules.

  WSGI is another standard that defines how web application backends written
  in Python can be served by web servers.

  **Google terms: 'http how does it work', 'apache http', 'ubuntu apache',
  'apache intall modules', 'apache wsgi'**

  If you haven't installed a web server before, don't despair and take the
  time to do a few of the simpler tutorials: set up a static web site, set
  up a 'Hello World' app with WSGI first.

  You also need to decide how you want to handle your python installation.
  The application needs external python libraries, and these can be installed
  globally, or locally to the application, e.g. with virtualenv. 

20. Addendum I: sending / delivering local email

  Some tasks ask for notification emails being sent in certain situations.

  For this to work, you need a local MTA (mail transport agent) to be installed
  that will accept and deliver the emails. The most popular alternatives on
  linux systems are sendmail, exim4 and postfix, of which I _think_ postfix is
  easiest to configure. The ubuntu package even contains a few default 
  configurations, of which 'local-only' is sufficient for this project.

  The choice of MTA is subjective, of course.

  If you want to learn more about email systems and the abbreviations used
  to describe them, **google 'mta mua'**. ('MUA' is the mail user agent, the 
  mail client an end user uses for handling email.)

  If you choose postfix, googling 'ubuntu postfix' will point you at the
  official ubuntu manual section.

  If you want to test your local mail setup, you can use the command 'mail'
  from the package 'bsd-mailx' to send an email from the command line.

  **Google terms 'linux send email command line'**

  Make sure to read the help articles you'll find to the end, the usage
  of 'mail' is not really intuitive, but it is a very helpful tool.

  (An alternative provider of the 'mail' command is the package GNU mailutils,
  but it will install more dependent packages, which is why I prefer 
  bsd-mailx'.

21. Addendum II: Reading local email

  For reading email on the command line, I prefer 'mutt', a very powerful
  text-based email client (MUA). If you already know the 'nano' text editor,
  you might want to check out 'pine' instead which has a similar user 
  interface.

  If you don't want to install a MUA, you can always read your email with
  less:

  **$ less /var/mail/grader**

  and **google 'linux mail spool'** for some background why it ends up there.
  
