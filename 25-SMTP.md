## Netcat Enumeration

    $ nc -vn [TARGET_IP] 25 

## NMAP Enumeration

    $ nmap -sV -script banner -p- [TARGET_IP]
    $ nmap -p25 --script smtp-commands [TARGET_IP]
    $ nmap -p25 --script smtp-open-relay [TARGET_IP] -v
    $ nmap --script smtp-enum-users [TARGET_IP]
    $ nmap --script=smtp-vuln-cve2010-4344,smtp-vuln-cve2011-1720,smtp-vuln-cve2011-1764 -p 25 [TARGET_IP]

## Available Default NMAP Scripts 

    smtp-brute.nse
    smtp-commands.nse
    smtp-enum-users.nse
    smtp-ntlm-info.nse
    smtp-open-relay.nse
    smtp-strangeport.nse
    smtp-vuln-cve2010-4344.nse
    smtp-vuln-cve2011-1720.nse
    smtp-vuln-cve2011-1764.nse 

Full Command: 

    $ nmap --script=smtp-commands,smtp-enum-users,smtp-vuln-cve2010-4344,smtp-vuln-cve2011-1720,smtp-vuln-cve2011-1764 -p 25 [TARGET_IP]

## Available Metasploit Auxiliary Modules 

    auxiliary/scanner/smtp/smtp_version
    auxiliary/scanner/smtp/smtp_ntlm_domain
    auxiliary/scanner/smtp/smtp_relay
    auxiliary/fuzzers/smtp/smtp_fuzzer
    auxiliary/scanner/smtp/smtp_enum
    auxiliary/dos/smtp/sendmail_prescan
    auxiliary/client/smtp/emailer
    auxiliary/server/capture/smtp

## Hydra Bruteforce 

    $ hydra -l <username> -P <Password_File> [TARGET_IP] smtp -V
    $ hydra -l <username> -P <Password_File> -s 587 [TARGET_IP] -S -v -V

## SMTP User Enumeration

    $ smtp-user-enum -U /usr/share/commix/src/txt/usernames.txt -t [TARGET_IP]
    $ smtp-user-enum -M VRFY -u root -t [TARGET_IP]
    
## Open mail relay with SMTP

    $ telnet [TARGET_IP] 25 
    HELO <name>@tester.com 
    mail from: <name>@tester.com
    rcpt to: <name>@<clientemaildomain>
    data
    Subject: Tester
    "If you can read this email it means that an open mail server was discovered. Please acknowledge receipt of email to <name>@tester.com. "
    .
    
### If successful, this will send an email to the client from the targeted host. 

This tactic should be conducted from the following contexts: 
  - External sender to internal recipient
  - Internal sender to external recipient
  - Internal sender to internal recipient

### SMTP Commands
  - HELO It’s the first SMTP command: is starts the conversation identifying the sender server and is generally followed by its domain name.
  - EHLO An alternative command to start the conversation, underlying that the server is using the Extended SMTP protocol.
  - MAIL FROM With this SMTP command the operations begin: the sender states the source email address in the “From” field and actually starts the email transfer.
  - RCPT TO It identifies the recipient of the email; if there are more than one, the command is simply repeated address by address.
  - SIZE This SMTP command informs the remote server about the estimated size (in terms of bytes) of the attached email. It can also be used to report the maximum size of a message to be accepted by the server.
  - DATA With the DATA command the email content begins to be transferred; it’s generally followed by a 354 reply code given by the server, giving the permission to start the actual transmission.
  - VRFY The server is asked to verify whether a particular email address or username actually exists.
  - TURN This command is used to invert roles between the client and the server, without the need to run a new connection.
  - AUTH With the AUTH command, the client authenticates itself to the server, giving its username and password. It’s another layer of security to guarantee a proper transmission.
  - RSET It communicates the server that the ongoing email transmission is going to be terminated, though the SMTP conversation won’t be closed (like in the case of QUIT).
  - EXPN This SMTP command asks for a confirmation about the identification of a mailing list.
  - HELP It’s a client’s request for some information that can be useful for the a successful transfer of the email.
  - QUIT 
