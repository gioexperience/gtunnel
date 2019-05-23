# gtunnel
## a smart script for making one, two or more reverse ssh tunnel, always open and reliable ##

I make this script because my RaspberryPI at home is behind an internet connection that not offer to me IP. This script (in *php language*) making tunnels direct to a public server and expose a local port to a remote port. In this way you can connect to a remote server to the remote port.... and you can connect to the local raspberry in the local port.

## Install something and understand schema ##

This script want php-cli, and sshpass

```console
foo@bar:~ $ sudo apt-get install -y sshpass php
```
You can see my blog for major details... www.gioexperience.com/xxxx


## Modify and insert your data ##

Obviosly you have to put into script some important things
- remote ip server (public ip)
- user on remote server (for login ssh)
- password for the user
- all tunnels in a php array

Open the script you can see

```php
$ip_server="";
$user = "";
$password = "";
$tunnels=array(
	array("192.168.0.1",80,47081),
	array("192.168.0.3",80,47080),
);
```

Modify it with your data.

## Usage for create tunnels ##

The first usage **start** create all tunnels and launch in background some process for keep it up. The main process NOT REMAIN in background...

```console
foo@bar:~$ ./gtunnel start
Test all tunnels. If only one is not active... reload all...
Tunnel on 47081 down. It's crashed?
Kill all tunnels for a complete reload
Starting tunnel from 192.168.0.1:80 and expose on xx.xx.xx.xx:47081...
exec] /home/pi/gtunnel start_single 192.168.0.1 80 47081
Starting tunnel from 192.168.0.3:80 and expose on xx.xx.xx.xx:47080...
exec] /home/pi/gtunnel start_single 192.168.0.3 80 47080
Tunnels reloaded...

foo@bar:~$
```

If you re-launch this **start**, the script check tunnels. If these tunnels are up, do nothing. If one tunnel is down, reload all.

```console
foo@bar:~$ ./gtunnel start
Test all tunnels. If only one is not active... reload all...
Tunnel on 47081 is up!
Tunnel on 47080 is up!
All tunnels are active. Do nothing...

foo@bar:~$
```
## Usage for kill all tunnels ##

The second usage is for kill al tunnels. Is useful for debug or other things. With one command you can kill ALL TUNNELS, ALL ssh process etc.

```console
pi@zm:~$ ./gtunnel kill
Kill all tunnels
pi@zm:~$
```
## Put gtunnel into crontab ##

The best use of this script is use in crontab. I have execute it every 5 minutes.

```console
pi@zm:~$ crontab -e

#add this line
* * * * * /home/pi/gtunnel start
```

## My Blog and My Experience ##

See my blog at www.gioexperience.com for more details and for more application, tips and tricks.
