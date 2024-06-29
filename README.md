# fttp-fedora
To set up a simple file sharing server on your Fedora system that can be accessed from other devices, you have a couple of options. I'll explain how to set up both an FTP server and an HTTP server:

1. Setting up an FTP server:



a) Install vsftpd (Very Secure FTP Daemon):
```
sudo dnf install vsftpd
```

b) Edit the configuration file:
```
sudo nano /etc/vsftpd/vsftpd.conf
```

c) Make sure these lines are uncommented or add them:
```
anonymous_enable=NO
local_enable=YES
write_enable=YES
chroot_local_user=YES
allow_writeable_chroot=YES
```

d) Start and enable the vsftpd service:
```
sudo systemctl start vsftpd
sudo systemctl enable vsftpd
```

e) Configure your firewall:
```
sudo firewall-cmd --add-service=ftp --permanent
sudo firewall-cmd --reload
```

2. Setting up an HTTP server:

For a simple HTTP server, you can use Python's built-in http.server module:

a) Navigate to the directory you want to share:
```
cd /path/to/your/directory
```

b) Start the Python HTTP server:
```
python3 -m http.server 8000
```

c) Configure your firewall:
```
sudo firewall-cmd --add-port=8000/tcp --permanent
sudo firewall-cmd --reload
```

To access your shared files:

- For FTP: Use an FTP client and connect to ftp://your_fedora_ip
- For HTTP: Open a web browser and go to http://your_fedora_ip:8000

Remember to replace "your_fedora_ip" with your actual local IP address.
