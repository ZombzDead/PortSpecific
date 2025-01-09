## TFTP Enumeration 

    $ tftp [TARGET_IP] PUT local_file
    $ tftp [TARGET_IP] GET conf.txt (or other files)

  Solarwinds TFTP server 

    $ tftp – i [TARGET_IP] GET /etc/passwd (old Solaris)

## Available Default NMAP Scripts

    $ nmap-n -Pn -sU -p69 -sV --script tftp-enum [TARGET_IP]
    $ nmap -sU -p 69 --script tftp-enum.nse --script-args tftp-enum.filelist=customlist.txt [TARGET_IP]

## Available Metasploit 
Checks if you can download/upload files to the system and TFTP Bruteforce.

    auxiliary/admin/tftp/tftp_transfer_util
    auxiliary/scanner/tftp/tftpbrute

## TFTP Commands 
Once access is gained, the following commands will be available.
  - send # Send single file
  - put # Send one file
  - mput # Send multiple files
  - mget # Get multiple files
  - get # Get file from the remote computer
  - ls # list
  - mget * # Download everything
  - binary = Switches to binary transfer mode
  - ascii = Switch to ASCII transfer mode
