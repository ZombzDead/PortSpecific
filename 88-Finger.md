## Available NMAP Scripts 
User enumeration

    $ nmap –p 88 –script-args krb5-enum-users.realm=’[TARGET_DOMAIN]’,userdb=[user list] [DC TARGET_IP] 

Brute Force Usernames

    $ nmap -p 88 --script=krb5-enum-users --script-args krb5-enum-users.realm="[TARGET_DOMAIN]",userdb={Big_Userlist} [TARGET_IP] 
 
## Available Metasploit Options
Enumerate valid Domain Users via Kerberos from a wholly unauthenticated perspective. It utilizes the different responses returned by the service to identify users that exist within the target domain.
    
    auxiliary/gather/kerberos_enumusers 

## Kerberos Brute force 

    $ kerbrute userenum -d [TARGET_DOMAIN] /usr/share/seclists/Usernames/xato-net-10-million-usernames.txt --dc [DC TARGET_IP]
