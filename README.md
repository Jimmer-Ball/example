This is an example project on github as created behind the corporate proxy in Bristol.

If you don't need to setup NTLM then you can skip directly to the section on installing
Git and go from there.  Please skip those steps that are NTLM specific, which are identified 
accordingly. 

Anyone who works in the UK will need to get this to work behind a corporate web proxy 
that uses the Windows NTLM authentication protocol for all outgoing HTTP requests.

NTLM is used for tracking the access of Windows users to the outside world,
so means providing a Windows domain, windows user-name and windows domain
password at the proxy.  The whole point of this corporate proxy is to track 
usage of the public internet by staff, to avoid any embarrassing security 
and usage issues by corporate users.

A) GitHub Setup
===============

We, as a company need to decide on whether we are using GitHub for exchange code or local SVN for
exchange code.  If using Git and GitHub this probably means paying for an Organisation account (see 
https://help.github.com/articles/what-s-the-difference-between-user-and-organization-accounts)
setting up GitHub properly, and each individual working on the project going through the
setup steps below.

We should also look at the branching and release strategies implied by using Git, see 
http://git-scm.com/book/en/Git-Branching-Branching-Workflows.

We need to ask the RoR guys what their branching and releasing strategy is, and evaluate it ourselves
and evaluate it for use on the exchange part of the project.

This guide assumes GitHub has been chosen, and all the security, availability, and branching issues 
this might cause us as a company have been resolved. 

So, only follow it if you need to setup Git with GitHub and Eclipse.

B) CNTLM Setup
==============
If you work in the UK, you'll need CNTLM.

1) Setup CNTLM locally on your windows box, available from http://sourceforge.net/projects/cntlm/files/
2) Add the proxy credentials to the INI file for CNTLM, as then you
   don't need to add it in Eclipse.  Set or add the following values 
   
	Username    <windows user name>
	Password    <windows user password>
	Domain		REBUSHR-UK
	Proxy		<proxy address and port applicable for UK site, e.g. srv-as22.uk.rebushr.com:80>
	Listen		8128
   
   
3) You could try setting CNTLM up with a domain, username, and password that doesn't have to
   change every time your windows domain user-name and password changes.  Chances
   are you will not be able to do this without asking IT for a magic username and password combination, 
   so will have to resort to remembering to change your cntlm INI setup every time your windows domain 
   password changes.
4) Run cntlm in the background by using the batch file holding the command "cntlm.exe -v -f -c cntlm.ini", or 
   do it directly from the windows command line.  If it starts good.  If it doesn't we'll have to work it out together.
5) Shutdown cntlm by exiting the run batch file (x on the window). 

C) Git installation and setup for git console access
====================================================

You can't use "git" for version control from the command line and from Eclipse means performing "git" client setup.  To do this 
means installation:

1) Navigate to http://git-scm.com/ or http://code.google.com/p/msysgit/downloads/list and download the latest stable
   release of "Download for Windows".  You'll see it on the RHS of the page.
2) Do the installation, by clicking on the down-loaded MSI file.
3) Then follow the basic setup guide at http://git-scm.com/book/en/Getting-Started-First-Time-Git-Setup.  If you are 
   using GitHub, then you should already have a username and a password for GitHub you can provide.  If you don't go and 
   get an account now at GitHub.  Note, how do we "control" usage of GitHub from a corporate perspective, or is that not 
   missing the point of GitHub completely?
4) Check your settings from the Git Console, which you'll find was installed to C:\Program Files (x86)\Git or a windows 64 bit
   box (send the "Git Bash" shortcut to your desktop if not already there) which is a cygwin console that comes with Git for 
   Windows.
5) Click on the "Git Bash" icon, if it starts you are getting there.  If it doesn't then we'll have to figure out what is happening 
   together.
6) In the console, type git --version, and then git config --list, and if you've not set your user details do so now, by typing

git config --global user.name "GitHub account username"
git config --global user.email youremail.as.known.for.github.account

7) So far so good. 

8) CNTLM SPECIFIC STEP: If you are behind a corporate proxy you need to set the HTTP proxy git uses from the command line to route via 
   CNTLM.  The easiest way is to exit the git console and navigate to the settings directory for git (e.g. C:\Users\<username>) and 
   update the file .gitconfig and add the following lines, evidently setting the NTLM proxy hostname to whatever it is and its port 
   number.

[http]
	proxy = localhost:8128
   
   Restart the git console, and now type git config --list, and check the http:proxy setting appears, as does the user.name and 
   user.email.
   
9) Okay, so now you can use git from the git console command line behind a CNTLM proxy.

10) CNTLM SPECIFIC STEP: Start cntlm, see step 4) in the previous section.

11) Try it out with a repository you've already created yourself at GitHub, by cloning locally, then committing locally, and then 
    putting to the remote server. If you don't know how, this is when you go and learn GitHub and accessing the remote repository 
    by cloning.  For cloning, and for putting the proxy settings using cntlm will be used, so you'll know if your setup works by
    this point.
    
12) If you are sharing a project with someone else, this is when you need to talk to them to decide on the name of the project and
    the access rights of users

D) Eclipse Setup
================

We have to install the EGit plugin for Eclipse to allow Eclipse to use.

1) CNTLM SPECIFIC STEP: Start CNTLM locally on your windows box if needed.
2) Start Eclipse
3) CNTLM SPECIFIC STEP: Configure Eclipse network connection to go via the CNTLM 
   proxy.  So, Window -> Preferences -> General -> Network Connection. First set the 
   "Active Provider" to "Manual", then add an HTTP entry for localhost, and set whatever
   port your CNTLM is running on. Set the Requires Authentication to false, as you've 
   already gone and added your authentication details to the CNTLM proxy INI file, so 
   don't need to repeat yourself here again.
7) Navigate to Help -> Install New Software.  Enter in http://download.eclipse.org/egit/updates
   in the "Work with" input field and hit return. This will prompt Eclipse to go via the proxy 
   (if configured) to get the plugin for EGit.
8) If the proxy is working you'll get two sets of items to choose from.  Choose them both, so ALL
   items are ticked.
9) Follow the instructions.
10) Check your settings.  Navigate to Window -> Preferences -> Team -> Git.  On the first panel provide a
    local disk location for your Git repositories (so where projects get cloned from GitHub locally), choosing
    a directory that you can navigate too. 
 
 E) Clone the shared project
 ===========================
 Now we have to clone the shared project on GitHub to somewhere local. 
 
 
 
 
  



Jim Ball (15/04/2013)
