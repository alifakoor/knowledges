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

#### SSH commands:

`ssh-keygen`: create a key pair for public key authentication

`ssh-copy-id`: configure a public key as authorized on a server

`scp`: file transfer client with RCP-like command interface

`sshd`: OpenSSH server, configuration

`rsync`: a fast, versatile, remote (and local) file-copying tool



معمولا جلوی لاگین با پسورد رو میگیریم و فقط اجازه میدیم که کانکشن ssh از طریق کلید انجام بشه

#### SSH Directory and Files:

