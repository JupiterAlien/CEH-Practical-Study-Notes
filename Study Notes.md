
# Certified Ethical Hacker (Practical) Notes - JupiterAlien

# Disclaimer: The information here stated is only for educational purposes. Do not use this for other purposes rather than education!

## Sudo overview

sudo --> run commands with elevated privileges
sudo cat /etc/shadow --> reading as root the elements on this directory

sudo su - --> change your current user to root user (careful here).

## Navigating the file system

pwd (present working directory) --> shows/prints in which folder you are
cd (change directory)  --> move between directories
cd /folderx/foldery 
cd .. --> move backwards
cd ~/FolderHere --> move to an specified folder without being in the parent directory
ls --> list items in a folder
ls -a --> list all items, even the hidden ones
ls -la --> list items with full details of them
mkdir --> create a folder
rmdir --> remove a folder
cp --> copy files 
cp [filenamehere] [destinationfolderhere]
rm Folder/File.ext --> remove an specific file in an specific folder
mv --> move files
locate --> locate a file within the system
updatedb --> updates everything for us, builds a database so that we can use locate with better results. 
man --> instructions/options/help on the commands used on the terminal
man [commandhere]
another option is [commandhere] --help

## Users and privileges

passwd --> changes the current user's password
adduser --> adds a new user
su [usernamehere] --> change between users
su root --> change to root user

![[ls -la.png]]

If there's a " - " at the beginning of the line, that means it is a file. 
If there's a " D " at the beginning of the line, that means it is a directory.

Permissions: 

r : Read permissions. The file can be opened, and its content viewed.
w : Write permissions. The file can be edited, modified, and deleted.
x : Execute permissions. If the file is a script or a program, it can be ran (executed).

""---" means no permissions have been granted at all.
"rwx"  means full permissions have been granted. The read, write, and execute indicators are all present.

These permissions are divided in groups of users

For instance, in drwxr-xr-x:

The first group, which is the owner of the file, has full read-write-execute permissions, (rwx).
The second group is the members of the group that owns the file, they have just read-execute permissions (r-x).
The third group are all other users, and in this case, they just have read-execute permissions (r-x). 

During penetration testing, we'll always look for full permissions. 

We can see these details by running ls -la and specify the folder. 
ls -la /tmp/

chmod --> change mode or change the permissions.
chmod 777 [fileorfolderhere] --> changed the permissions to rwx.

## Common Network Commands

ifconfig --> displays all the interfaces types information.
iwconfig --> displays wireless interfaces information.

arp -a --> shows IP addresses and its associated MAC address.

netstat -ano --> shows the active connections on the host.

route --> prints the routing table

ip a --> displays the interfaces information, the updated version of ifconfig.
ip n --> displays the arp table, the updated version of arp -a.
ip r --> displays the routing table, the updated version of route.

## Installing and updating tools

apt install [toolname] --> installs the desired tool.
apt update && apt upgrade --> updates/upgrades the current version of the distro, install the new packages. 

apt install python-pip --> installs the Python package manager or modules, a python interpreter if you like. 

Pimp my kali by Dewalt, this script fixes common issues with Kali. Also helps to downgrade tools' versions.

A good practice when installing tools, is to install them into /opt.

git clone [githubURLhere] --> installs tools from Github.

./scriptname --> command to run a shell script.

apt install gedit --> installs another text editor.


## Viewing, creating and editing files

echo "whatever you want here" > filename.txt --> this creates a txt file with the string you stated between quotes.
echo "info here" >> filename.txt --> this makes an append to the existing file. 

cat filename.txt --> reads and displays the information on the file. 

useful example:  

	echo "192.168.1.10" > ipsgathered.txt
	echo "10.10.5.1" >> ipsgathered.txt

touch newfile.txt --> another way to create a file
nano thisisanewfile.txt --> creates and edit a new file using nano

The usage of gedit make things easier when editiing files due to its GUI. 

grep --> utilized to extract specific string portions on a file. 

	cat ip.txt | grep "64 bytes"

cut --> cuts out something from a file
cut -d --> is a delimiter
cut -d -f --> -f is a switch for field

cat ip.txt | grep "64 bytes" | cut -d " " -f 4 --> on this example I'm setting a space as a delimiter and counting to 4 to obtain what's in that field

tr --> translate, useful to remove noisy values
tr -d ":" --> on this case, we are using tr as a "replace/remove" function, eliminating the : on the string
cat ip.txt | grep "64 bytes" | cut -d " " -f 4 | tr -d ":"

## Scripting with bash

ping x.x.x.x -c 1 --> send just one package, I can play around with the count (-c) number.

ping x.x.x.x -c 2 > ping.txt --> stores the result of that ping in a txt file. 

mousepad --> another text editor, useful to create scripts. 

mousepad ipsweep.sh --> creates a script file and opens the text editor. 

#!/bin/bash --> use this at the beggining to declare that this is a shell script and it will be ran from there. 

Once done declaring this, I can paste cat ip.txt | grep "64 bytes" | cut -d " " -f 4 | tr -d ":" through the text editor to create a script with these commands. 

So the script will look like this: 

	#!/bin/bash

	for ip in `seq 1 254`; do
	ping -c 1 192.168.25.$ip | grep "64 bytes" | cut -d " " -f 4 | tr ":" &
	done

What this script is doing is: for the stated sequence, go through 1 to 254, pinging or sending just one package, then narrow down the information, provide the value on field 4 and finally remove the ":". Also this is making a counn of the pinged IPs leveraging $ip. 

./ipsweep --> that's how I can run the script

	#!/bin/bash

	for ip in `seq 1 254`; do
	ping -c 1 $1.$ip | grep "64 bytes" | cut -d " " -f 4 | tr ":" &
	done

By changing the IP for $1, this means that it will run the argument 1. This script will walk through the network listing the IPs that responded to the ping. 

Please remember to give the proper permissions to the script.
chmod +x ipsweep.sh --> add execution privilege the current owner user of the specified file

An improved version of the previous script will be: 

	#!/bin/bash

	if [ "$1" == ""]
	then
	echo "You forgot an IP address"
	echo "Syntax: ./ipsweep.sh IP.address.here"

	else
	for ip in `seq 1 254`; do
	ping -c 1 $1.$ip | grep "64 bytes" | cut -d " " -f 4 | tr ":" &
	done
	fi

This will help me to handle errors in some fashion.

So I can use this script to gather all the IP addresses on the network and store them in a txt file

./ipsweep.sh 192.168.25 > ipsfound.txt

One line script to have nmap checking the IPs I've gathered

	for ip in $(cat ipsfound.txt); do nmap $ip & done

## Python scripting

**How to create a basic port scanner**

	gedit portscanner.py&

Once the text editor is up:

	#!/bin/python3

	import sys
	import socket
	from datetime import datetime

	if len(sys.argv) == 2:

		target = socket.gethostbyname(sys.argv[1]) ## This translates hostname to IPv4
	else:

		print("Invalid amount of arguments.")
		print("Syntax: python3 portscanner.py <ip>")

	print("-" * 50) 
	print("Scanning target " + target)
	print("Time started: " + str(datetime(now)))
	print("-" * 50) 

	try: 

		for port in range(50,85):
			s = socket.socket(socket.AF_INET,socket.SOCK_STREAM)
			socket.setdefaulttimeout(1) ## this sets the timeout range so that we don't wait forever
			result = s.connect_ex((target,port)) ## returns an error indicator
			if result == 0:
				print("Port {} is open".format(port))
			s.close
		
	except KeyboardInterrupt:
		print("\nExiting program".)
		sys.exit()
	
	except socket.gaierror:
		print("Hostname couldn't be resolved.")
		sys.exit()
	
	except socket.error:
		print("Couldn't connect to server.")
		sys.exit()


## Ethical Hacker Methodology


#### The information here stated will be used only for educational purposes. 


**5 stages of the ethical hacking**

Information Gathering or Reconnaissance: Active vs Pasive
Scanning & Enumeration
Gaining Access (Exploitation)
Maintaining Access
Covering Tracks


## Information Gathering or Reconnaissance (Passive Recon)

#### Physical / Social

Location information: satellite images, drone recon, building layout (badge readers, break areas, security, fencing)

Job information: employees (names, job title, phone numer, email address), pictures (badges, photos, desk photos, computer photos)

This kind of information is super useful to execute further actions. 

#### Web / Host

Target validation: WHOIS, nslookup, dnsrecon
Finding sub-domains: Google Fu, dig, Nmap, Sublist3r, Bluto, crt.sh
Fingerprinting: Nmap, Wappalyzer, WhatWeb, BuiltWith, Netcat
Data breaches: HaveIBeenPwned, Breach-Parse, WeLeakinfo


## Identifying our target

Side note: Bugcrowd is a good place to start reading and learning about the bug bounty programs. 

#### Email Address Gathering with Hunter.io

This site (hunter.io) gives us email addresses of our target, including its sources, the most common pattern of the email address, departments, job titles. 

#### Gathering breached credentials with Breach-Parse

