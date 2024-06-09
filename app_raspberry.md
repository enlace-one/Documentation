# Hardening

## Updates
I tried unattended-upgrade but they lock the system so it can't install or shut down for hours.

For now, I run this when I log in:
```
sudo apt update -y && sudo apt upgrade -y
```

## Firewall
```
sudo apt install ufw
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw limit ssh
sudo ufw allow http
sudo ufw allow https
sudo ufw logging on
sudo ufw enable
```

## Restrict SSH
### Prevent Root SSH
```
sudo nano /etc/ssh/sshd_config
```
Change  `PermitRootLogin` to `no` and ensure it is uncommented.
### User Certificates
I tried this as well but ended up not being able to use certificates yet. Still working on it.

## Handle root
I did not have to do this, but if root was ever enabled, it should be disabled. 

# Sources
https://chrisapproved.com/blog/raspberry-pi-hardening.html 
