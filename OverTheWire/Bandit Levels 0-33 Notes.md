### Level 0: 
**Solution**: 
**Commands**:
1. ls
2. cat readme
**Password**: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If

### Level 1: 
**Solution**: 
**Commands**:
1. ls
2. cat ~/-
**Password**: 263JGJPfgU6LtdEvgfWU1XP5yac29mFx

### Level 2: 
**Solution**: 
**Commands**:
1. ls
2. cat ~/-- spaces\ in\ this\ filename
**Password**: MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx 

### Level 3: 
**Solution**: 
**Commands**:
1. ls -la
2. cd ~/inhere
3. ls -la
4. pwd
5. cat /home/bandit3/inhere/...Hiding-From-You
**Password**: 2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ

### Level 4: 
**Solution**: 
**Commands**:
1. ls -la
2. cd ~/inhere
3. ls -la
4. pwd
5. cat /home/bandit4/inhere/-file07
**Password**: 4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw

### Level 5: 
**Solution**: 
**Commands**:
1. ls -la
2. cd ~/inhere
3. ls -la
4. cd maybehere07
5. ls -la
6. pwd
7. cat /home/bandit5/inhere/maybehere07/.file2
**Password**: HWasnPhtq9AVKe0dmk45nxy20cvUa6EG

### Level 6: 
**Solution**: 
**Commands**:
1. ls -la
2. find / -type f -user bandit7 -group bandit6 -size 33c  
3. cat /var/lib/dpkg/info/bandit7.password 
**Password**: morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj 

### Level 7: 
**Solution**: 
**Commands**:
1. ls -la
2. grep "millionth" ~/data.txt
**Password**: dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc

### Level 8: 
**Solution**: 
**Commands**:
1. ls -la
2. sort ~/data.txt | uniq -u
**Password**: 4CKMh1JI91bUIZZPXDqGanal4xvAg0JM

### Level 9: 
**Solution**: 
**Commands**:
1. ls -la
2. strings -a ~/data.txt | grep "="
**Password**: FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey

### Level 10: 
**Solution**: 
**Commands**:
1. ls -la
2. base64 -d ~/data.txt
**Password**: dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr

### Level 11: 
**Solution**: 
**Commands**:
1. ls -la
2. cat ~/data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
**Password**: 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4

### Level 12: 
**Solution**: 
**Commands**:
1. ls -la
2. cd /tmp
3. mkdir workspace
4. cd workspace
5. cp ~/data.txt /tmp/workspace
6. file data.txt
7. cat data.txt
8. cat data.txt | xxd -r > hexed.gz
9. file hexed.gz
10. gunzip hexed.gz
11. bunzip2 hexed
12. file hexed.out
13. mv hexed hexed.gz
14. gunzip hexed.gz
15. file hexed
16. tar -x -f hexed
17. file data5.bin
18. tar -x -f data5.bin
19. file data6.bin
20. bunzip2 data6.bin
21. file data6.bin.out
22. tar -x -f data6.bin.out
23. file data8.bin
24. mv data8.bin data8.bin.gz
25. gunzip data8.bin.gz
26. file data8.bin
27. cat data8.bin
**Password**: FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn

### Level 13: 
**Solution**: 
**Commands**:
1. ls -la
2. scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private .
3. Input password
4. sudo chmod 700 sshkey.private
5. ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
**Password**: MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS

### Level 14: 
**Solution**: 
**Commands**:
1. ls -la
2. nc localhost 30000
**Password**: 8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
 
### Level 15: 
**Solution**: 
**Commands**:
1. ls -la
2. ncat --ssl localhost 30001
**Password**: kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx

### Level 16: 
**Solution**: 
**Commands**:
1. ls -la
2. nmap -p 31000-32000 localhost
3. ncat --ssl localhost 31790
4. exit
5. cd ~/.ssh
6. echo "insert private key from command" > sshkey1.private
7. sudo chmod 700 sshkey1.private
8. ssh -i sshkey1.private bandit17@bandit.labs.overthewire.org -p 2220
**Password**: EReVavePLFHtFlFsjn3hyzMlvSuSAcRD 

### Level 17: 
**Solution**: 
**Commands**:
1. ls -la
2. diff --suppress-common-lines passwords.old passwords.new
**Password**: x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO

### Level 18: 
**Solution**: 
**Commands**:
1. ssh -p 2220 bandit18@bandit.labs.overthewire.org 'cat readme'
2. enter password
**Password**: cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8

### Level 19: 
**Solution**: 
**Commands**:
1. ls -la
2. ~/bandit20-do cat /etc/bandit_pass/bandit20
**Password**: 0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO

### Level 20: 
**Solution**: 
**Commands**:
1. ls -la
2. echo "0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO" | nc -l -p 1234 &
3. ~/suconnect 1234
4. ps aux | grep "nc"
5. kill "insert pid"
**Password**: EeoULMCra2q0dSkYj561DX7s1CpBuOBt

### Level 21: 
**Solution**: 
**Commands**:
1. ls -la
2. cd /etc/cron.d
3. ls -la
4. cat cronjob_bandit22
5. cat /usr/bin/cronjob_bandit22.sh
6. cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
**Password**: tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q

### Level 22: 
**Solution**: 
**Commands**:
1. ls -la
2. cd /etc/cron.d
3. ls -la
4. cat cronjob_bandit23
5. cat /usr/bin/cronjob_bandit23.sh
6. cat /tmp/8ca319486bfbbc3663ea0fbe81326349
**Password**: 0Zf11ioIjMVN551jX3CmStKLYqjk54Ga

### Level 23: 
**Solution**: 
**Commands**:
1. ls -la
2. cd /etc/cron.d
3. ls -la
4. cat cronjob_bandit24
5. cat /usr/bin/cronjob_bandit24.sh
6. mkdir -p /var/spool/bandit24/foo
7. cat << 'EOF' > /var/spool/bandit24/foo/getpass.sh
#!/bin/bash
cat /etc/bandit_pass/bandit24 > /tmp/bandit24pass
EOF
8. chmod 777 /var/spool/bandit24/foo/getpass.sh
9. touch /tmp/bandit24pass
10. chmod 666 /tmp/bandit24pass
11. Wait 1 minute (cat /tmp/bandit24pass)
**Password**: gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8

### Level 24: 
**Solution**: 
**Commands**:
1. ls -la
2.
``` bash 
cat << 'EOF' > /tmp/brute24.sh
#!/bin/bash

PASSWORD="gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8"
HOST="localhost"
PORT=30002

# Generate all 10000 combinations and pipe them in one connection
for i in $(seq -w 0000 9999); do
    echo "$PASSWORD $i"
done | nc $HOST $PORT | grep -v "Wrong\|Please"

EOF
```
3. chmod +x /tmp/brute24.sh
4. bash /tmp/brute24.sh
**Password**: iCi86ttT4KSNe1armKiwbQNmB3YJP3q4

### Level 25: 
**Solution**: 
**Commands**:
1. ls -la
2. cat /etc/passwd | grep bandit26
3. cat /usr/bin/showtext
4. scp -P 2220 bandit25@bandit.labs.overthewire.org:bandit26.sshkey .
5. Input password
6. sudo chmod 700 bandit26.sshkey
7. Shrink terminal window to less than 6 lines vertically
8. ssh -i bandit26.sshkey bandit26@bandit.labs.overthewire.org -p 2220
9. v
10. :set shell=/bin/bash
11. :shell
12. cat /etc/bandit_pass/bandit26
**Password**: s0773xxkk0MXfdqOfPRVr9L3jJBUOgCZ

### Level 26: 
**Solution**: 
**Commands**:
1. scp -P 2220 bandit25@bandit.labs.overthewire.org:bandit26.sshkey .
2. Input password
3. sudo chmod 700 bandit26.sshkey
4. Shrink terminal window to less than 6 lines vertically
5. ssh -i bandit26.sshkey bandit26@bandit.labs.overthewire.org -p 2220
6. v
7. :set shell=/bin/bash
8. :shell
9. ls
10. ./bandit27-do cat /etc/bandit_pass/bandit27
**Password**: upsNCc7vzaRDx6oZC6GiR6ERwe1MowGB

### Level 27: 
**Solution**: 
**Commands**:
1. ls -la
2. On local Machine: nano ~/.ssh/config
3. Add the below
```
Host bandit
    HostName bandit.labs.overthewire.org
    Port 2220
    User bandit27-git
```
1. mkdir ~/myrepo27
2. cd ~/myrepo27
3. git clone ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo .
4. ls -la
5. cat README
**Password**: Yz9IpL0sBcCeuG7m9uQFt8ZNpS4HZRcN

### Level 28: 
**Solution**: 
**Commands**:
1. ls -la
2. On local Machine: nano ~/.ssh/config
3. Add the below
```
Host bandit
    HostName bandit.labs.overthewire.org
    Port 2220
    User bandit28-git
```
1. mkdir ~/myrepo28
2. cd ~/myrepo28
3. git clone ssh://bandit28-git@bandit.labs.overthewire.org:2220/home/bandit28-git/repo .
4. ls -la
5. cat README.md
6. git log
7. git show 00daa614aac60bd2981c381484191eb7bc4dcfd9
**Password**: 4pT1t5DENaYuqnqvadYs1oE4QLCdjmJ7

### Level 29: 
**Solution**: 
**Commands**:
1. ls -la
2. On local Machine: nano ~/.ssh/config
3. Add the below
```
Host bandit
    HostName bandit.labs.overthewire.org
    Port 2220
    User bandit29-git
```
1. mkdir ~/myrepo29
2. cd ~/myrepo29
3. git clone ssh://bandit29-git@bandit.labs.overthewire.org:2220/home/bandit29-git/repo .
4. ls -la
5. cat README.md
6. git log
7. git branch -a
8. git checkout /remotes/origin/dev
9. git log
10. git show 4a8f414d4587ca65b6f9512bf690ca0d885e8933
**Password**: qp30ex3VLz5MDG1n91YowTv4Q8l7CDZL
### Level 30: 
**Solution**: 
**Commands**:
1. ls -la
2. On local Machine: nano ~/.ssh/config
3. Add the below
```
Host bandit
    HostName bandit.labs.overthewire.org
    Port 2220
    User bandit30-git
```
1. mkdir ~/myrepo30
2. cd ~/myrepo30
3. git clone ssh://bandit30-git@bandit.labs.overthewire.org:2220/home/bandit30-git/repo .
4. ls -la
5. cat README.md
6. git log
7. git tag
8. git show secret
**Password**: fb5S2xb7bRyFmAvQYQGEqsbhVyJqhnDy

### Level 31: 
**Solution**: 
**Commands**:
1. ls -la
2. On local Machine: nano ~/.ssh/config
3. Add the below
```
Host bandit
    HostName bandit.labs.overthewire.org
    Port 2220
    User bandit31-git
```
1. mkdir ~/myrepo31
2. cd ~/myrepo31
3. git clone ssh://bandit31-git@bandit.labs.overthewire.org:2220/home/bandit31-git/repo .
4. ls -la
5. cat README.md
6. git log
7. echo "May I come in?" > key.txt
8. git add -f key.txt
9. git config --global user.email "bro@youwish.com"
10. git config --global user.name "Bro Shi"
11. git commit -m key.txt
12. git push origin
**Password**: 3O9RfhqyAlVBEZpVb6LYStshZoqoSx5K

### Level 32: 
**Solution**: 
**Commands**:
1. $0
2. ls -la
3. cat /etc/bandit_pass/bandit33
**Password**: tQdtbs5D5i2vJwkO8mEyYEyTL8izoeJ0

### Level 33: 
**Solution**: 
**Commands**:
1. ls -la
2. cat README.txt
**Final Completion Message**:
Congratulations on solving the last level of this game!

At this moment, there are no more levels to play in this game. However, we are constantly working
on new levels and will most likely expand this game with more levels soon.
Keep an eye out for an announcement on our usual communication channels!
In the meantime, you could play some of our other wargames.

If you have an idea for an awesome new level, please let us know!

