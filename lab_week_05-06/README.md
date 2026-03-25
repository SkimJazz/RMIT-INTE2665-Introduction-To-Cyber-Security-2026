# RMIT - INTE2665 Intro to Cyber Security Lab Workshops Weeks 5-6

This week (5-6), we will focus on Internet Protocol (IP) security and firewalls. The key activities include:

1. Exploring IP security and IPSec  

2. Examining firewall roles and functions  

3. Reflecting on ethics and cybercrime  

4. Applying packet filtering firewalls (iptables) – Part 1  

Recommended tasks:  

- Review Week 5 materials for deeper understanding.  

- Complete tasks on IPSec basics (5.1.2), evaluate packet filtering firewall ruleset (5.2.4), and practice with iptables (5.4.1).  


## Packet Filtering Firewalls (IPTABLES)

In the Kali Linux VM, perform the following commands to check iptables and save/restore existing rules.

1. Check if iptables is already installed and running on the system.

   `dpkg -l | grep iptables`

2. Install iptables (if not installed).

   `sudo apt-get install iptables`

3. See which rules are already added in the firewall.

   `sudo iptables -S`

Whats this for?

The command `sudo iptables -S` is used in Unix-like operating systems to display the current firewall 
rules configured with iptables. The `iptables` utility manages the Linux kernel's packet filtering and 
NAT (Network Address Translation) rules. The `-S` (or `--list-rules`) option lists all rules in a 
format that shows the exact commands needed to recreate them. Using sudo ensures the command runs with 
administrative privileges, which are required to view or modify firewall rules. This command is helpful 
for system administrators who want to review, audit, or back up the current firewall configuration.

4. Save the existing rules in a text file.

   `sudo iptables-save > firewall.rules`

   > Note: firewall.rules is a sample text file.

5. Load/restore existing rules from a text file.

   `sudo iptables-restore < firewall.rules`

   > Note: firewall.rules is a sample text file where firewall rules are saved.

## Basic syntax

    `iptables -A <chain> -j <target>`

What is this for?



The command `iptables -A <chain> -j <target>` is used to add a new rule to a specific chain in the Linux firewall system called iptables. Here, `-A` stands for "append," which means the rule will be added to the end of the specified chain. The <chain> placeholder should be replaced with the name of the chain you want to modify, such as `INPUT`, `OUTPUT`, or `FORWARD`. The `-j` option specifies the "jump" target, which tells iptables what action to take if a packet matches this rule. Common targets include `ACCEPT` (allow the packet), `DROP` (block the packet), or `REJECT` (block and notify the sender). 


### Chains

These are 3 predefined chains in the filter table to which we can add rules, for processing IP packets passing through those chains. These chains are:

- INPUT - All packets destined for the host computer.
- OUTPUT - All packets originating from the host computer.
- FORWARD - All packets neither destined for nor originating from the host computer but passing through (routed
  by) the host computer. This chain is used if you are using your computer as a router.

### Target

Built in targets are ACCEPT, DROP and RETURN.

- **ACCEPT** - Accept the packet and stop processing rules in this chain.
- **DROP** - Drop the packet and stop processing rules in this chain.
- **RETURN** - If the end of a built-in chain is reached or a rule in a built-in chain with target RETURN is matched, the target specified by the chain policy determines the fate of the packet.

  > You can use `man iptables` to check other parameters.

## iptables examples

> **Accept TCP packets on destination port 22 (SSH) from IP address 192.168.10.5**

`sudo iptables -A INPUT -p tcp -s 192.168.10.5 --dport 22 -j ACCEPT`

## Explanation

- `INPUT` means all packets destined for the host computer.
- `ACCEPT` means accept the packet (for each rule there is an action to ACCEPT or to DROP a packet).
- `-p tcp` means the protocol is TCP.
- `--dport 22` means the destination port is 22.
- `-s` means the source IP address (if this part is omitted or `-s 0/0` is used then the rule is for any source IP). Same is for `-d`.

Below are some standard ports.

- `HTTP: 80`
- `HTTPS: 443`
- `FTP: 21`
- `SSH: 22`
- `Telnet: 23`
- `SMTP: 25`
- `POP3: 110`
- `MySQL: 3306`

You can check the following link for details of a port number and other commonly used port numbers. https://www.cloudflare.com/en-au/learning/network-layer/what-is-a-computer-port/

## Misc commands

1. How to see line numbers with the rules
   
   `sudo iptables -L --line-number`

   Chain INPUT (policy ACCEPT)

   num target prot opt source destination

   1 ACCEPT tcp -- 192.168.1.1 anywhere tcp dpt:ssh Chain FORWARD (policy ACCEPT)

   num target prot opt source destination Chain 
   
   OUTPUT (policy ACCEPT)

   num target prot opt source destination

2. How to delete a particular rule number

   Use below command to delete rule 1.

   `sudo iptables -D INPUT 1`

3. How to delete all rules

   `sudo iptables -F`

## Check and test services

You can use the following commands to check SSH, HTTP and MySQL services.

### SSH server

1. Check if server is installed

   `cat /etc/services | grep ssh`

   or
   
   `ls /etc/init.d/ssh`

   If script exists, it means SSH Server is installed.

2. Check if server is running

   `/etc/init.d/ssh status`

   If it shows SSH is active, it means SSH server is running.

3. Start the server

   Otherwise use the following command to start server.

   `/etc/init.d/ssh start`

### Web server

1. Check if server is installed

   `cat /etc/services | grep http`

   or
   
   `ls /etc/init.d/apache2`

   If script exists, it means Web Server (Apache) is installed.

2. Check if server is running

   `/etc/init.d/apache2 status`

   If it shows Apache HTTP server is active, it means Web Server is running.

3. Start the server

   Otherwise use the following command to start server.

   `/etc/init.d/apache2 start`

### MySQL server

1. Check if server is installed

   `cat /etc/services | grep mysql`

2. Check if server is running

   `service mysql status`

   If it shows MySQL is inactive, it means MySQL server is running.

3. Start the server

   Otherwise use the following command to start server.

   `service mysql start`


## Enable MySQL server to be connected from other computers


### Bind Address

Append below two lines in `/etc/mysql/my.cnf` file, so that MySQL connection can be made from other computers from network.

`[mysqld]`

`bind-address=0.0.0.0`

> Make sure you restart MySQL Server after making this change.

### User Access

Connect with MySQL server.

`mysql -uroot -p`

Execute following commands in MySQL shell so that MySQL can be connected with MySQL root user.

`GRANT ALL ON _._ TO root@localhost;`

`FLUSH PRIVILEGES;`

Execute following commands in MySQL shell so that MySQL can be connected with MySQL root user from any computer.

`GRANT ALL ON _._ TO root@'%';`

`FLUSH PRIVILEGES;`

Now three servers `HTTP`, `SSH` and `MySQL` are ready for **iptables practice**.


## Connecting to other servers


### SSH server

Use the following command to check that you may connect to other servers with SSH.

`ssh root@192.168.112.4`

Here root is the username and **192.168.112.4** is IP address of the server where you want to connect with SSH.

### Web server

`wget http://192.168.112.4`

or

`curl http://192.168.112.4`

Or you can check `http://192.168.112.4` URL in the browser.

Here **192.168.112.4** is IP address of the Web server where you see a web page.

### MySQL server

`mysql -uroot -p -h192.168.112.4`

Here root is the username of MySQL and **192.168.112.4** is IP address of the MySQL Server where you want to connect.
