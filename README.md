#Windows #

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
