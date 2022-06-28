# The smbclient is a client that is part of the Samba software suite. It communicates with a LAN Manager server, offering an interface similar to that of the ftp program. 

## Operations include things like getting files from the server to the local machine, putting files from the local machine to the server, retrieving directory information from the server and so on.

## Here's a list of the most common commands


List shares on a machine using NULL Session

    smbclient -L <target-IP>
  
List shares on a machine using a valid username + password

    smbclient -L <target-IP> -U username%password
    
Connect to a valid share with username + password

    smbclient //targetshare$ -U username%password
    
List files on a specific share

    smbclient //targetshare$ -c 'ls' password -U username
    
List files on a specific share folder inside the share

    smbclient //targetshare$ -c 'cd folder; ls' password -U username
    
Download a file from a specific share folder

    smbclient //targetshare$ -c 'cd folder;get desired_file_name' password -U username
    
Copy a file to a specific share folder

    smbclient //targetshare$ -c 'put /var/www/my\_local\_file.txt .\target\_folder\target\_file.txt' password -U username

Create a folder in a specific share folder

    smbclient //targetshare$ -c 'mkdir .\target\_folder\new\_folder' password -U username

Rename a file in a specific share folder

    smbclient //targetshare$ -c 'rename current\_file.txt new\_file.txt' password -U username


    
