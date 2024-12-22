# Writeup

## Level 0

Using ssh command to connect to the host on port 2220 with username `bandit0`. 
```bash
$ ssh bandit0@bandit.labs.overthewire.org -p 2220 -l bandit0
```

## Level 1

After logging onto the SSH server, simply did:
```bash
$ ls
```
In order to find what files are present in the current home directory, found a file named `readme`.

Now used:
```bash
$ cat readme
```
And successfully got the password:
```
ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
```

## Level 2

After logging in as `bandit1`, listed the files in the home directory:
```bash
$ ls
```
Found a file named `-`.

Used this to read the file:
```bash
$ cat ./-
```

Successfully obtained the password:
```
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
```

## Level 3

After logging in as `bandit2`, open the file with spaces

Displayed its contents:
```bash
$ cat "spaces in this filename"
```
Successfully obtained the password:
```
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
```

## Level 4

After logging in as `bandit3`, stayed in the `inhere` directory:
```bash
$ cd inhere
```
Listed all files (also hidden) :
```bash
$ ls -al
```
Used the `cat` command to open the hidden file:
```bash
$ fcat ...Hiding-From-You
```
Successfully obtained the password:
```
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
```

## Level 5

After logging in as `bandit4`, navigated to the `inhere` directory:
```bash
$ cd inhere
```
```bash
$ ls -a
```
```bash
$ file ./-*
```
then open the ASCII text file (file07) using cat 

Successfully obtained the password:
```
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
```

## Level 6

After logging in as `bandit5`,
```bash
$ cd inhere
```
```bash
$ find . -type f -size 1033c ! -executable
```
Found the file `./maybehere07/.file2`

Displayed its contents:
```bash
$ cat ./maybehere07/.file2
```
Successfully obtained the password:
```
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```

## Level 7

After logging in as `bandit6`, 
```bash
$ find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
```
Found a file named `/var/lib/dpkg/info/bandit7.password`.

```bash
$ cat /var/lib/dpkg/info/bandit7.password
```
Successfully obtained the password:
```
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
```

## Level 8

After logging in as `bandit7`, listed the files in the home directory:
```bash
$ ls
```
Found a file named `data.txt`.

Used `grep` to find the line containing "millionth":
```bash
$ grep "millionth" data.txt
```
Output:
```
millionth	dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```
Successfully obtained the password:
```
dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```

## Level 9

After logging in as `bandit8`, listed the files in the home directory:
```bash
$ ls
```
Found a file named `data.txt`.

Used `sort` and `uniq` to find the unique line:
```bash
$ sort data.txt | uniq -u
```
Output:
```
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```
Successfully obtained the password:
```
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```

## Level 10

After logging in as `bandit9`, listed the files in the home directory:
```bash
$ ls
```
Found a file named `data.txt`.

Used `strings` and `grep` to find the password preceded by `=`:
```bash
$ strings data.txt | grep '='
```
Output:
```
}========== the
p\l=
;c<Q=.dEXU!
3JprD========== passwordi
qC(=	
~fDV3========== is
7=oc
zP=	
~de=
3k=fQ
~o=0
69}=
%"=Y
=tZ~07
D9========== FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
N=~[!N
zA=?0j
```
Successfully obtained the password:
```
FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
```

## Level 11

After logging in as `bandit10`, listed the files in the home directory:
```bash
$ ls
```
Found a file named `data.txt`.

Decoded the Base64 content:
```bash
$ cat data.txt | base64 --decode
```
Output:
```
The password is dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```
Successfully obtained the password:
```
dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```

## Level 12

After logging in as `bandit11`, listed the files in the home directory:
```bash
$ ls
```
Found a file named `data.txt`.

Decoded the ROT13 content:
```bash
$ cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```
Output:
```
The password is 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```
Successfully obtained the password:
```
7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```

## Level 13

After logging in as `bandit12`, listed the files in the home directory:
```bash
$ ls
```
Found a file named `data.txt`.

```bash
$ mkdir /tmp/srijan
$ cp data.txt /tmp/srijan
$ cd /tmp/srijan
$ ls
$ file data.txt
$ xxd -r data.txt data1
$ file data1
$ mv data1 data2.gz
$ gzip -d data2.gz
$ file data2
$ mv data2 data3.bz2
$ bzip2 -d data3.bz2
$ file data3
$ mv data3 data4.gz
$ gzip -d data4.gz
$ file data4
$ tar -xvf data4
$ file data5.bin
$ tar -xvf data5.bin
$ file data6.bin
$ mv data6.bin data7.bz2
$ bzip2 -d data7.bz2
$ file data7
$ tar -xvf data7
$ file data8.bin
$ mv data8.bin data9.gz
$ gzip -d data9.gz
$ file data9
```

Displayed the final password:
```bash
$ cat data9
```
Successfully obtained the password:
```
FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn
```

## Level 14

After logging in as `bandit13`, listed the files in the home directory:
```bash
$ ls
```
Found a file named `sshkey.private`.

Now used scp to transfer from `bandit13` to local

```bash
$ scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private .
```

Set the correct permissions for the SSH key:
```bash
$ chmod 600 sshkey.private
```

Used the SSH key to log in as `bandit14`:
```bash
$ ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
```

Once logged in, read the password file:
```bash
$ cat /etc/bandit_pass/bandit14
```
Successfully obtained the password:
```
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
```

## Level 15

After logging in as `bandit14`, submitted the current password to port `30000` using `nc` (netcat):
```bash
$ echo "MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS" | nc localhost 30000
```
Response:
```
Correct!
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
```
Successfully obtained the password:
```
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
```
