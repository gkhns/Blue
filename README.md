#Windows #

**NMAP Scan**

```sh
  nmap -sV -sC -p- 10.10.207.235
  ```

- To see the versions of the services running (**-sV**)
- To perform a script scan using the default set of scripts (**-sC**)
- To scan all ports from 1 through 65535 (**-p-**)

OPEN PORTS

* 22/tcp ssh
* 80/tcp http

![image](https://user-images.githubusercontent.com/99097743/171080626-c28a88e2-45bf-4be1-a7f1-6d927ee7b2b8.png)


Interesting info: A person named Jessie is mentioned in the website source code:

![image](https://user-images.githubusercontent.com/99097743/171075119-d4d404da-8220-4061-ad97-5bd0af1dd0eb.png)

Let's try **Nikto** for vulnerability scanning. 
