# Writeup Taming i-CTFF8

## 📑 Table of Contents

- [Forensics](#forensic)
  - [73 Golongan Manusia Di Akhirat](#73golongan)
  - [Khutbah Jumaat](#khutbah)
  - [Guest Zip & OS What](#Guest-Zip&OS-What)
  - [Help me!](#Help-me!)


### 73 Golongan Manusia Di Akhirat
### Khutbah Jumaa
### Guest Zip & OS What

We were given an encrypted 7-Zip archive.
First, I extracted the archive’s password hash using 7z2john so it could be cracked offline with John the Ripper.

![.](forensic/Guest-Zip&OS-What/7z2john.png)
This converts the 7z encryption metadata into a crackable hash format.

Next, I tried a wordlist attack using the popular rockyou.txt wordlist.
However, this took a long time and didn’t return any result. I assumed the password was not present in rockyou.txt, which is common in CTF challenges.

Instead of brute-forcing blindly, I generated my own wordlist.
I used keywords such as event names, question name, event venue.

![.](forensic/Guest-Zip&OS-What/passlist.png)

Using the custom wordlist, I ran John again:

![.](forensic/Guest-Zip&OS-What/wordlist.png)
This time, the password was cracked successfully.

password: **`ictff8`**

With the password, I extracted the contents of the archive:
1. ictff8.img
2. ictff8.vmdk
3. ictff8.vmx
4. ictff8.vmxf

These files indicate a virtual machine disk.

![.](forensic/Guest-Zip&OS-What/file.png)

I opened the disk image using Autopsy and performed keyword searches.
After analyzing the contents, I was able to locate the flag successfully.
![.](forensic/Guest-Zip&OS-What/autopsy.png)

#### 🚩 Flag: ictf8{win3.1win}
#

### Help me!
