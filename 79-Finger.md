## Available Default NMAP Scripts 

    $ nmap -sV -p 79 –Pn [TARGET_IP] 

## Finger Banner Grab 

    $ nc -vn [TARGET_IP] 79
    $ echo "root" | nc -vn [TARGET_IP] 79

## User Enumeration 
Get list of users or specific user

    $ finger @[TARGET_IP]
    $ finger admin@[TARGET_IP]
    $ finger user@[TARGET_IP]

Solaris Bug: 

    $ finger 0@[TARGET_IP] 

SunOS: RPC services allow user enum 

    $ rusers
    $ finger 'a b c d e f g h'@[TARGET_IP]  

## Available Metasploit Auxiliary Modules

    auxiliary/scanner/finger/finger_users
    auxiliary/gather/mybb_db_fingerprint
    auxiliary/scanner/finger/finger_users
    auxiliary/scanner/oracle/isqlplus_login
    auxiliary/scanner/oracle/isqlplus_sidbrute
    auxiliary/scanner/vmware/esx_fingerprint
    auxiliary/server/browser_autopwn 

## Available Metasploit Exploit Modules

    exploit/bsd/finger/morris_fingerd_bof
    exploit/windows/http/bea_weblogic_post_bof
    post/windows/gather/enum_putty_saved_sessions
