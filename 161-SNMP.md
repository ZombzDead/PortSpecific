# 161 - SNMP
SNMP (Simple Network Management Protocol) is running on the port 161/UDP or 500 (VPN). Simply, it allows you to view what’s going on the devices (computers, printers etc) on your network and fix issues before they become the major problem. SNMP stands for Simple Network Management Protocol and consists of three key components: managed devices, agents, and network-management systems (NMSs). 

**Reference:** https://resources.infosecinstitute.com/snmlsp-pentesting/#gref

## SNMP Enumeration 

    $ snmpwalk -c public -v1 [TARGET_IP]
    $ snmpwalk [APPLICATION OPTIONS] [COMMON OPTIONS] [OID]
    $ snmpcheck -t [TARGET_IP] -c public
    $ snmp-check [TARGET_IP] -c public
Note: you can change the word  public of the first line of /etc/snmp/snmpd.conf 

    $ snmpenum -t [TARGET_IP]
    $ ./snmpenum.pl [TARGET_IP] public cisco.txt
    $ ./snmpenum.pl [TARGET_IP] public linux.txt
    $ ./snmpenum.pl [TARGET_IP] public windows.txt 

### Braa Mass SNMP Scanner

    $ braa [-2] [-v] [-t <s>] [-f <file>] [-a <time>] [-r <retries>] [-d <delay>] [querylist1] [querylist2] 

SNMP Enumeration 

    $ python /usr/share/doc/python-impacket/examples/samrdump.py [TARGET_IP]

### OneSixtyOne

    $ onesixtyone [TARGET_IP] public
    $ onesixtyone [options] [TARGET_IP] <community string private or public>
    $ cat /usr/share/doc/onesixtone/dict.txt 
    $ onesixtyone [TARGET_IP] -c /usr/share/doc/onesixtyone/dict.txt 


**Reference:** 
- https://github.com/PentestBox/snmpwalk.git
- https://github.com/ajohnston9/snmpenum/blob/master/snmpenum.pl
- https://github.com/mteg/braa
- https://github.com/trailofbits/onesixtyone

## Available NMAP Options

    $ nmap -sU [TARGET_IP] -p161
    $ nmap [TARGET_IP] -Pn -sU -p 161
    $ nmap [TARGET_IP] -Pn -sU -p 161 --script=snmp-info
    $ nmap -sT -p 161 [TARGET_IP] -oG snmp_results.txt
    $ # sudo nmap -sU [TARGET_IP] -p161 --script=snmp-brute -Pn --script-args snmp-brute.communitiesdb=list.txt

To see more SNMP Scripts, navigate to /usr/share/nmap/scripts;  # ls | grep 'snmp'

## SNMP Inspect Traffic 

    Wireshark > snmp filter

## Available Metasplolit Options

    auxiliary/scanner/snmp/snmp_enum
    auxiliary/scanner/snmp/snmp_enumshares
    auxiliary/scanner/snmp/snmp_enumusers
    auxiliary/scanner/snmp/snmp_login 

Wordlist - /usr/share/metasploit-framework/data/wordlists/snmp_default_pass.txt

**Reference:** https://exploitstube.com/exploiting_snmp.html

## Brute Force Options

    msf> use auxiliary/scanner/snmp/snmp_login
    $ nmap -sU --script snmp-brute [TARGET_IP] [--script-args snmp-brute.communitiesdb=<wordlist> ]
    $ onesixtyone -c /usr/share/metasploit-framework/data/wordlists/snmp_default_pass.txt [TARGET_IP]
    $ hydra -P /usr/share/seclists/Discovery/SNMP/common-snmp-community-strings.txt [TARGET_IP] snmp
