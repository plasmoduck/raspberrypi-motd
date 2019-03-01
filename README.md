motd
====

#### Message of the Day for the Raspberry Pi ####

<p align="center">
  <img src="https://github.com/plasmoduck/raspberrypi-motd/blob/master/motd.png?raw=true"/>
</p>

Written in bash and tested with the Raspbian distribution.

Just clone the repositoy `git clone https://github.com/plasmoduck/raspberrypi-motd/` then set the execution permissions and change the owner:
```bash
cd  /path/to/raspberrypi-motd/
sudo chown root:root motd.sh
sudo chmod +x motd.sh
``` 

- Autoexecute the script when the user logs in via a tty console or ssh

I found that the previous method of placing the script in `/etc/profile.d/` leads to the desktop login manager getting stuck in an endless loop asking for password in Raspbian.

However, the script `motd.sh` should not be exicuted by placing in `/etc/profile`. The correct method is to source the `motd.sh` script in the file `~/.profile` by placing a link to it at the end of the file like `/path/to/motd.sh` and it will be executed after login.

Be sure to remove the default MOTD.
  
  ```bash
  $ sudo rm /etc/motd
  ```
  
- You can remove the "last login" information. However it is considered a security risk. If you wish to do so, you should disable the `PrintLastLog` option from the `sshd` service. Edit the `/etc/ssh/sshd_config` file and uncomment the line `#PrintLastLog yes`:
  
  ```bash
  $ sudo nano /etc/ssh/sshd_config
  ```
  
  Before:
  
  ```text
  #PrintLastLog yes
  ```
  
  After:
  
  ```text
  PrintLastLog no
  ```
  
  Restart the `sshd` service:
  
  ```bash
  $ sudo /etc/init.d ssh restart
  ```
Now simply SSH into the Pi and see the beautiful MOTD. Have fun =)

Note: If you don't see the degree Celsius character correctly (`º`) make sure you have enabled a UTF8 locale.
