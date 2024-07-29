Setting up an SSH (Secure Shell) connection between two servers is a straightforward process. Here's a basic outline of the steps you'll need to follow:

1. **Check for Existing SSH Keys**: First, you need to check if you already have SSH keys on your local server (the server you are connecting from). SSH keys are a pair of cryptographic keys that can be used to authenticate to an SSH server as an alternative to password-based logins.
    - Open a terminal on your local server.
    - Run the command `ls -al ~/.ssh` to see if existing SSH keys are present.
    - Look for files named `id_rsa.pub` or `id_dsa.pub`. If you see such files, you already have an SSH key.
    
1. **Generate a New SSH Key**: If you don't have an SSH key, you'll need to generate one.
    - Run `ssh-keygen -t rsa -b 4096 -C "your_email@example.com"` in the terminal. Replace `"your_email@example.com"` with your email address. This command creates a new SSH key, using the provided email as a label.
    - When prompted to "Enter a file in which to save the key," press Enter to accept the default file location.
    - At the prompt, enter a secure passphrase.
    
1. **Copy the SSH Key to Your Remote Server**: Now, you need to copy the public key to the remote server (the server you want to connect to).
    - Use the command `ssh-copy-id user@remote_server_ip`. Replace `user` with the remote username and `remote_server_ip` with the server's IP address.
    - If `ssh-copy-id` is not available, you can manually copy the key by displaying its contents with `cat ~/.ssh/id_rsa.pub` and pasting them in the remote server's `~/.ssh/authorized_keys` file.
    
1. **Login to Your Remote Server**: Once the key is copied, you can log in to your remote server without a password.
    - Use the command `ssh user@remote_server_ip`. Again, replace `user` with the remote username and `remote_server_ip` with the server's IP address.
    
1. **Troubleshooting**: If you cannot connect, ensure that the SSH service is running on the remote server and the SSH port (usually port 22) is open. Also, check the firewall settings on both the local and remote servers to make sure they allow SSH connections.

Remember, the specifics can vary depending on your server's configuration and the operating system. Make sure that the SSH service is installed and running on both servers. If you encounter any issues, the error messages are usually quite informative, so they can guide you towards resolving any problems.


متداول‌ترین روشی که ما به سرورها وصل میشیم و با اونها صحبت می‌کنیم، ssh هستش
ما راه ورودمون به سرور رو باید امن کنیم تا وقتی که بهش وصل میشیم دچار اختلال نشیم
در سرورها اینطوریه که اگر تنها ورود رو بزاریم ssh و اون رو هم امن کنیم تا حد خوبی سرور ما امن میشه

جایی که ازش داریم ssh میزنیم رو بهش میگیم client و جایی که داریم بهش ssh میزنیم بهش میگیم سرور، ممکنه شما از یه سرور دیگه ssh بزنی ولی در اون لحظه اون سرور میشه client

### SSH Directory and Files:
هر کاربر در مسیر `/home/[username]` یک دایرکتوری داره به نام `.ssh` که در آن یکسری فایل قرار میگیره
یکی از این فایل‌ها `authorized_keys` هستش که public key ما اگر بخواهیم به این سرور ssh بزنیم در این فایل قرار میگیره
برای اینکه public keyتون رو به این فایل در سرور مدنظرتون اضافه کنید، یه حالت اینکه محتوای این فایل رو کپی کنید و در اون فایل کپی کنید، و یه حالتم اینکه از دستور `ssh-copy-id user@ip` استفاده کنید

فایل `known_hosts` هم یک فایل ssh client هستش که شامل تمامی سرورهای وصل شده است


### SSH Commands:

`ssh-keygen`: create a key pair for public key authentication

`ssh-copy-id`: configure a public key as authorized on a server

`scp`: file transfer client with RCP-like command interface

`sshd`: OpenSSH server, configuration

`rsync`: a fast, versatile, remote (and local) file-copying tool


معمولا جلوی لاگین با پسورد رو میگیریم و فقط اجازه میدیم که کانکشن ssh از طریق کلید انجام بشه


`ssh user@ip`

`ssh user@ip -p [port]`

`ssh -i [path_to_pem_file] user@ip`

`ssh user@ip 'ls -l'`

`ssh user@ip bash < script.sh`

`ssh user@ip "tar -cvzf - ~/ffmpeg" > output.tgz`

`ssh-copy-id user@ip`
`ssh-copy-id -i [path_to_public_key] user@ip`


نکات:
- بهینه است که پورت پیش‌فرض ssh که ۲۲ هستش را عوض کنیم
- به صورت کلی دستور ssh به صورت `ssh user@ip [options] [commands]` هستش که میتوانید یه کامند را در سروری که به آن ssh می‌زنید، اجرا کنید و اگر کامند نزنید، یک محیط bash از آن سرور میگیرد و در اختیار شما می‌گذارد


#### SSH keygen:
می‌توان با استفاده از دستور `ssh-keygen` یک جفت کلید ssh ساخت
![[Pasted image 20240729102842.png]]

نکات:
- می‌توان public key را از روی private key ساخت اما برعکس امکان‌پذیر نیست
- مقدار passphrase پسورد این private key هستش، که اگر به کلی هم دسترسی پیدا کرد، نتونه ازش استفاده کنه
- می‌توان passphrase و comment را عوض کرد برای یک کلید
- می‌توان کلید را با الگوریتم‌ و طولهای مختلف ساخت
- 

#### [[SSH agent]]


### Advanced SSH Commands:
![[Pasted image 20240729104904.png]]



### SSH jumping

به سروری که ما به اون دسترسی داریم و اون به جاهای دیگه‌ای دسترسی داره میگیم bastion
![[Pasted image 20240729112015.png]]

مطابق تصویر بالا، فرض کنید که شما به یک سرور دسترسی دارین که نقش سرور bastion رو بازی میکنه، یا اصطلاحا یه دستش تو public network هستش و یه دستش تو private network
ولی شما به target server که در private network هست، دسترسی ندارین و فقط به bastion server دسترسی دارین
حالا برای اینکه به target server دسترسی پیدا کنیم، میتونیم از ssh jumping استفاده کنیم
چیکار میکنه؟ میاد وقتی که شما ssh می‌زنید به سرور bastion، کانکشن شما میپره میره روی target server

میتونیم این کار رو با دستور زیر انجام بدیم:
```sh
ssh -J user1@server1 user2@server2
```

نکته:
این ssh jumping برای امن کردن سرورهامون خوبه، معمولا ما همه سرورهامون رو داخل یک private network میزاریم و فقط یک سرور bastion میاریم که از طریق اون دسترسی داشته باشیم
و روی امنیت و فایروال اون سرور bastion خیلی کار میکنیم، تا انتها hardening رو براش اجرا میکنیم


### SSH tunneling

![[./files/Pasted image 20240729121328.png]]

![[./files/Pasted image 20240729121430.png]]

نکته:
- میشه با `-L` یه پورت بفرستیم روی سرور مقصد
- میشه با `-R` یه پورت از سرور مقصد رو بیارم روی کلاینت
- میشه با `-D` تمام پروت‌ها رو بفرستیم روی سرور مقصد


![[./files/Pasted image 20240729121829.png]]

![[./files/Pasted image 20240729122418.png]]

نکته جالب:
با استفاده از دستور `curl ifconfig.io` می‌توان ip که از بیرون میتونن ما رو با اون ببینن رو بدست بیاریم


### SSH Config

کانفیگ‌های مربوط به daemon یا سرویس ssh در مسیر `/etc/ssh/sshd_config` هستند
این کانفیگ خیلی کانفیگ مهمیه، و سعی میکنیم همیشه درست کانفیگش کنیم و خیلی امنیت خوبی بهمون میده

از مواردی که در ssh توصیه میشه حتما کانفیگ کنید:
- port
- ip address
- password auth
- login with key
- user and group
- ssh banner

**نکته:**
قبل از ریستارت کردن سرویس ssh باید حتما با دستور `sshd -t` فایل کانفیگ ssh رو چک کنیم، تا اگر مشکل سینتکس یا مشکل دیگه‌ای داشتیم، سرویس رو ریستارت نکنیم و دیگه بالا نیاد

میتونیم در قسمت PasswordAuthentication در فایل sshd_config جلوی لاگین با پسورد رو بگیریم و فقط با کلید متصل بشیم

جزو best practiceهای هاردنینگ این هستش که در فایل sshd_config مواردی مثل AllowAgentForwarding, AllowTcpForwarding, X11Forwarding رو مقدار no میزاریم

یا یکی دیگه از این موارد اینکه از کانفیگ AllowUsers استفاده کنید تا کاربرانی که فقط میتوانند از طریق ssh به سرور دسترسی داشته باشند رو مشخص کنیم

بهتره که ssh banner رو هم کانفیگ کنیم، ssh banner اون اطلاعاتی هستش که در ابتدای اینکه به سرور ssh میزنیم نمایش داده میشه، بهتره کانفیگ کنیم بابت اینکه اگر اطلاعات حساسی داریم روی سرور، کسی که کانکشن میزنه رو مطلع کنیم از این قضیه تا اگر دو روز دیگه در دادگاه گفت که من اطلاعی نداشتم ازینکه این سرور حساسه، نتونه
با ویرایش دو فایل `/etc/issue` و `etc/issue.net` این بنر رو تغییر بدیم، در واقع هر چی تو این دو تا فایل هست در ssh banner نمایش داده میشه
و در کانفیگ ssh، در فایل sshd_config هم باید در قسمت Banner آدرس این فایل رو بدیم


### SSH config in client:
`~/.ssh/config`

![[./files/Pasted image 20240729125836.png]]


![[./files/Pasted image 20240729154026.png]]
