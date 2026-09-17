Basic SSH Discovery
nmap -p 22 <IP>

Service and Version Detection
nmap -sV -p 22 <IP>

Default Safe SSH Scripts
nmap -sV --script ssh* -p 22 <IP>

Enumerate SSH Host Keys
nmap --script ssh-hostkey -p 22 <IP>

Check Supported Authentication Methods
nmap --script ssh-auth-methods -p 22 <IP>

Enumerate SSH Algorithms/Ciphers
nmap --script ssh2-enum-algos -p 22 <IP>

Aggressive Enumeration
nmap -A -p 22 <IP>

Scan a Subnet for SSH
nmap -p 22 10.10.10.0/24

Find OpenSSH Versions Across a Network
nmap -sV --open -p 22 10.10.10.0/24

NSE Scripts Commonly Used Against SSH
nmap --script ssh-auth-methods -p 22 <IP>
nmap --script ssh-hostkey -p 22 <IP>
nmap --script ssh2-enum-algos -p 22 <IP>
nmap --script banner -p 22 <IP>

Full SSH Enumeration One-Liner
nmap -sV -Pn -p 22 --script ssh-hostkey,ssh-auth-methods,ssh2-enum-algos,banner <TARGET>

nmap -sV -Pn -p 22 --script ssh2-enum-algos,ssh-hostkey,ssh-auth-methods <IP>
