motd
====

#### Message of the Day for the Raspberry Pi ####

<p align="center">
  <img src="https://github.com/gagle/raspberrypi-motd/blob/master/motd.png?raw=true"/>
</p>

Written in bash and tested with the Raspbian distribution.
```
Just clone the repositoy `git clone https://github.com/plasmoduck/raspberrypi-motd/` then set the execution permissions and change the owner:
```bash
$ sudo chown root:root motd.sh
$ sudo chmod +x motd.sh
``` 

````
- Autoexecute the script when the user logs in via a tty console or ssh

I found that the previous method of placing the script in `/etc/profile.d/` leads to the desktop login manager getting stuck in an endless loop asking for password in Raspbian.

However, the script `motd.sh` should not be exicuted by placing in `/etc/profile`. The correct method is to source the `motd.sh` script in the file `~/.profile` and it will be executed after the login.

Be sure to remove the default MOTD. It is located in `/etc/motd`.
  
  ```bash
  $ sudo rm /etc/motd
  ```
  
- Remove the "last login" information. Disable the `PrintLastLog` option from the `sshd` service. Edit the `/etc/ssh/sshd_config` file and uncomment the line `#PrintLastLog yes`:
  
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
  $ sudo systemctl restart sshd
  ```

Note: If you don't see the degree Celsius character correctly (`º`) make sure you have enabled a UTF8 locale ([Arch Linux locales](https://wiki.archlinux.org/index.php/locale)).
