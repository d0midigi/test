# Google Hacking Cheat Sheet

**Google Advanced Search Operators**

**Search Service**

**Search Operators**

Web Searches

allinanchor:, allintext:, allintitle:, allinurl:, cache:, define:, filetype:, id:, inurl:, link:, related:, site:

Image Searches

allintitle:, allinurl:, filetype:, inurl:, intitle:, site:

Groups

allintext:, allintitle:, author:, group:, insubject:, intext:, intitle:

Directories

allintext:, allintitle:, allinurl:, ext:, filetype:, intext:, intitle:, inurl:

News

allintext:, allintitle:, allinurl:, intext:, intitle:, inurl:, location:, source:

Product Searches

allintext:, allintitle:

LIST OF SEARCH OPERATORS

COMMAND

DESCRIPTION

Allinanchor:

This operator restricts results to pages containing all query terms specified in the anchor text on links to the page

Example: \[ allinanchor: best museums puerto rico]

Allintext:

This operator restricts results to those containing all the query terms specified in the test of the page

Example: \[ allintext: travel packing list]

Allintitle:

This operator restricts results to those containing all the query terms specified in the title

Example: \[allintitle: detect plagiarism]

Allinurl:

This operator restricts results to those containing all the query terms specified in the URL

Example: \[allinurl: google faq]

Author:

This operator will restrict your Google Groups results to include newsgroup articles specified by the author

Example: \[ children author:john author:doe] or \[ children author:doe@someaddress.com]

Cache:

This operator displays Google’s cached version of a webpage, instead of the current version of the page

Example: \[cache:www.eff.org]

Define:

This operator shows definitions from pages on the web for the term that follows

Example: \[ define:blog]

Ext:

This is an undocumented alias for filetype:

Filetype:

This operator restricts your Google Groups results in newsgroup articles from certain groups or subareas

Example: \[sleep group:misc.kids.moderated]

Id:

This is an undocumented alias for info:

Inanchor:

This operator restricts the results to pages containing the query terms you specify in the anchor text or links to the page

Example: \[restaurants inanchor:latin cuisine]

Inurl:\~/ftp//193 filetype:(php | txt | html | asp | xml | cnf | sh) \~’/html’

Returns a list of FTP servers by IP address, mostly Windows NT servers with guest login capabilities

Intitle:”index of” share.passwd OR cloud.passwd OR [ftp.passwd-public](ftp://ftp.passwd-public/)

Dorks containing passwords

-pub -pool intitle:”index of” db.key OR server.key OR [ftp.key](ftp://ftp.key/) OR exchange.key OR host.key OR mail.key

This dork will give you a lot of private keys (also known as secret keys, or a secret key)

intitle:”index of” “ftp.log”

Dorks containing FTP logs

intitle:”index of” “ws\_ftp.log”

Finds sensitive directories

Intitle:”index of” inurl:ftp intext:logs

Finds files containing juicy information

Site:ftp.\* index of /ftp/backup

View \*Backup\* files on \*FTP\* servers of various websites

Site:ftp://ftp.\*.\*/login -inurl:https://

Finds login portals

Intitle:”index of” “ftp.passwd”

Finds files containing passwords

Inurl:ftp://ftp

Detects live FTP sites

Inurl:ft;://ftp robots.txt

Finds robots.txt in FTP sites

“/FTPSVC2” intitle:”index of”

Finds open Microsoft FTP server logs

Inurl:”/cgi-bin/WS\_FTP.LOG”

Find field in cgi-bin directory

Intitle:ProFTPD Admin – v1.04

Will show you an admin page, no login needed

Intext:”softperms.txt” ext:TXT

Will generate juicy information that may lead to a parent directory, for best practice, filter according to the country

Intitle:”Index Of” intext:ftpconfig

Retrieves FTP/SFTP credentials in the ftpconfig file from the Atom text editor

“\[FFFTP]” ext:ini

Finds files with FTP logins, server information, and more

Inurl:”http://ftp.dlink”

Finds lists of FTP directories of D-Link routers

Inurl:proftpdpasswd

Dork of proftpd passwords

“\[HKEY\_CURRENT\_USER\Software\sota\FFFTP]” filetype:reg

Finds files with valuable information about Windows servers

Intext:”Powered by net2ftp”

Web-based FTP client login pages

Inurl:”ftp” intext:”user” | “username” | “userID” | “user ID | “logon” | “login” intext:”password” | “passcode” | “passphrase” | filetype:xls | filetype:xlsx

Retrieves passwords

inurl:ftp inurl:Seagate

inurl:Backup inurl:Plus

inurl:Drive

Finds open Seagate NAS drives

filetype:xml inurl:/WEB-INF/

inurl:ftp:// -www

Finds sensitive and interesting information under WEB-INF directory via the FTP protocol

Inurl:ws\_ftp.ini: “\[WS\_FTP]”

Filetype:ini

Finds files containing various device passwords

Google Dork

**Description**

“Sorting Logs:” “Please enter your password” “Powered By” -urlscan -alamy

Finds stealer botnet control panels

Intitle:”Authorization” “TF”

Inurl:”admin.php”

Finds a bunch of unprotected botnet control panels

Ext:php intext:”-rwxr-xr-x”

Site:in

Discover affected and vulnerable software

Intitle:index of

Intext:@WannaDecryptor@.exe

More information about the WannaCry Ransomware

Intitle:index of intext:wncry

Dork to find servers affected by the WannaCry Ransomware

Inurl:”go.cgi?url=”

Dork to find servers affected by the WannaCry Ransomware

“WHMCS Auto Exploiter”

Finds WHMCS exploit shell in sites

“El Moujahidin Bypass Shell” ext:php

Simple upload/dir shell

( ext:php ) (inurl: /wp-content/uploads/AAPL/loaders/ )

Finds some handy web shells

Inurl:?filesrc=\*\*\*\* \~”Current” \~”:/” \~”upload”

Finds extensive lists of shell backdoors implemented on websites

“File Manager Version 1.0”

“Coded By”

Finds file managers web shells

Inurl:”html/js/editor/ckeditor/”

Finds liferay upload file

“You have selected the following files for upload (0 Files).”

Finds file upload pages

Intitle:”nstview v2.1::

Nst.void.ru” | intext:”nsTView v2.1 :: nst.void.ru. Password: Host:”

Web shell

Filetype:php intext:Your Email:

Intext:Your Name

Intext:Reply-To: intext:mailer

Results in PHP mailers

Intitle:”Hamdida X\_Shell Backd00r”

Backdoor

“Fenix Final Version v2.0”

Filetype:php

Web Shell

Intitle: Automatic cPanel Finder/Cracker | 3xp1r3 Cyber Army

An exploit to find uploaded cPanel Finders/Crackers scripts and to find cracked cPanels in them

Inurl:revslider inurl:temp

Inurl:update\_extract

Inurl:sym1

Symlinks to files using the revslider vulnerability

Intitle:”Shell I”

Inurl:revslider inurl:error.php

Inurl:cmd

Finds shells inserted using the revslider vulnerability

Intext:Developed By Black.Hack3r ext:php

Upload Shell Dorks

Ext:aspx intitle:aspxspy

ASP shells

Intext:”Sw Bilgi” ext:php

Upload Shell Dorks

Intext:”Thehacker – Agd Scorp – BLaSTER – Cr@zy\_King – KinSize – JeXToXiC – s3f4 – rx5”

BLaSTER Webshell Footholds

Intext:”Please select file to upload” ext:php

Various file upload forms

“index of” / lck

These lock files often contain usernames of the user that has the locked file

Inurl:admin filetype:asp

Inurl:userlist

Reveals user lists of administrative importance. User lists found using this method can range from benign “message group” lists to system user lists containing passwords

Inurl:admin inurl:userlist

Reveals user lists of administrative importance. User lists found using this method can range from benign “message group” lists to system user lists containing passwords

Intitle:index.of .bash\_history

The file contains what a user typed at a shell command prompt

Intitle:index.of .sh\_history

Consists of what a user typed at a shell command prompt

**Sensitive Directories**

**Google Dork**

**Description**

Intitle:”index of” “/Cloudflare-CPanel-7.0.1”

Exposes Cloudflare CPanel sensitive files

-pool intitle:”index of” wget-log -pub

Provides good insight into what was downloaded in a system

Intitle:”index of” “sms.log”

Contains SMS logs

Intitle:”index of” “ftp.log”

Contains FTP logs

-pub -pool intitle:”index of”

Vagrantfile –“How to”

The primary function of the Vagrantfile is to describe the type of machine required for a project, and how to configure and provision these machines. It can contain DB passwords, private keys, usernames, and more

Intitle:”index of”

.oracle\_jre\_usage/

Provides version of Java used by the target entity, if installed

-pub -pool intitle:”index of” squirrelmail/

Squirrel mail configuration files and sometimes credentials

Intitle:”index of” api\_key OR “api\_key” OR apiKey

API keys

Intitle:”index of” .zshrc\~ OR .zshrc OR .zshenv\~ OR .zshenv -pool -public

Z Shell (zsh) juicy information

Intitle:”index of” domain.key -public

Domain private keys

“key” OR key.jar intitle:”index of” webstart

**Java Web Start** (also known as **JavaWS, javaws,** or **JAWS**) allows users to start application software from the Java Platform directly from the Internet using a web browser.

Index of /storage/logs

Provides informational Logs of the Laravel framework

Intitle:index of “chroot.conf”

Contains sensitive information

Intitle:index of “uploads”

The file contains juicy information

Intitle:”index of” “ws\_ftp.log”

Sensitive FTP directories

Intitle:index of “htaccess.txt”

Contains htaccess.txt cleartext sensitive information

Intext:”index of” intext:..bak

Intext:config

Div backup files

Intext:”Sw Bilgi” ext:php

Upload Shell Dork

Intitle:”index of” .cpanel/caches/config”

CPanel Caches Config Directory Listing

intitle: "Index of" intext:log

File Containing Juicy Info - Dorks allow you to view logs. (e.g./log, file/log, ftplogs, server logs

intitle:"Directory Listing For" "Filename" intext:Tomcat/5.0.28

Access the sensitive directories of any web application using Apache Tomcat/5.0.28

intitle: "index of" "includes"

Access the sensitive directories (includes, wp-includes) using “includes" file

intitle:"index of" "db"

Access the sensitive directories using “db" file

inurl:/uploads/wc-logs

WooCommerce Classes PayPal Payment Information

inurl:/files/conta

Shows some pdf files used in contao CMS

inurl:typo3conf/l10n/

Directories from typo3 cms exploiting directory listing

intitle:"index of" ".dockerignore"

Access the Sensitive Directories using .dockerignore file

intitle:"index of" "/aws.s3/"

Access the Sensitive Directories of Amazon-Web-Services

intitle:"index of" ".pem"

Access the. pem (Privacy Enhanced Mail) file

intitle:"index of" "/bitcoin/"

Access the Sensitive Directories using bitcoin directories

“description" & "size" intitle:"index of" "owncloud"

Owncloud folders

"Last modified" intitle:"index of" "dropbox"

Dropbox folders

inurl:"/cgi-bin/CVS/"

Find files in cgi-bin directories

"sasl\_passwd" | smtpd.conf intitle:"index of"

Postfix sensitive files, also passwords

intitle:"index of" "/user" | "/users"

Shows existing users in the system by simply going to the above-aforementioned directories

intitle:"index of" inurl:documents backup

Backup folders containing some interesting information

inurl:"/.Trash" intitle:"index of" \~

Some juicy information in some \*nix trash bins

intitle:"index of" $Recycle.bin

Interesting information in some Windows recycle bins

intitle:"index of" "/Windows/Recent" | "/Windows/History/"

Can access most recently used files and historical data

intitle:"index of" "WindowsCookies"

Retrieve cookies from Windows users

intitle:"index of" "Application Data/Microsoft/Credentials"

Dork for finding private directories inside wordpress-popup plugin including admin data which are present in Wordpress websites

allinurl:"wp-content/plugins/wo xrdpress-popup/views/admin/"

Dork for finding private directories inside wordpress-popup plugin including admin data which are present in WordPress websites

allintitle:"Index of /ThinkPHP" | inurl: "/ThinkPHP/"

Obtain -Webserver Version - SSH Version - SSH Keys - SSH Logins - SSH .exe files

intitle:"Index Of" intext:".Trash"

Dorks containing trash folders on Linux/Unix machines

intitle:CV+index of

Search and download CV from web director

inurl:"apps/backend/config/" ViewVC

View repository listing

intext:"Powered by ViewVC" | intitle:"ViewVC Repository Listing"

ViewVC Repository Listing

“lv\_poweredBy”

Folders with lots of shared files

Intext:”/wp-content/uploads/wpsc/”

Generates juicy information

Returns files shared in Network File Systems (NFS)

Create own shortcuts using aliases and shell functions. Aliases can be declared in BASH files

Generate juicy information to user files

Generate juicy information in the parent directory, for best practice filter according to the country

Generate juicy information in the parent directory, for best practice filter according to the country

Probable symbolic links to the root file system of the web server that can be browsable

Obtain private database details including SQL and other database elements and contents
