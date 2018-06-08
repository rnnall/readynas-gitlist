# gitlist ReadyNAS setup

This is a an experiement with creating github repository on a NetGear ReadyNAS 104 system. Utlimate goal will be to sync with **Google Drive** and considering: Dropbox, Box, OneDrive...

## System Information

**Model:** ReadyNAS 104

**Firmware Name:** ReadyNASOS

**Firmware Version:** 6.9.3

 **Memory:** 512

## Installation

TODO: Describe the installation process

### Dependancy

PHP: Install from RadyNAS addon apps form Devloper: Poussin

![php](images/2018/06/php.png)

#### Errors

_ERROR:_ Please, edit the config file and provide your repositories directory

_FIX:_ Permisions on `/home/<username>`  `drwx------ 1 git   users` to `drwx------ 1 git   users` with <kbd>chmod 755 /home/git/</kbd>

_ERROR:_ When selecting repository http://192.168.80.128:7082/gitlist/
> **Not Found**
>
> The requested URL /gitlist/ was not found on this server.

_FIX:_ use the `index.php` path http://192.168.80.128:7082/index.php

## Usage

TODO: Write usage instructions

## Contributing

1. Fork it!
2. ...

## History

TODO: Write history

## Credits

TODO: Write credits

TODO https://gofedora.com/how-to-install-configure-gitweb/

TODO https://gofedora.com/insanely-awesome-web-interface-git-repos/

TODO https://community.netgear.com/t5/Using-your-ReadyNAS/OS-6-1-4-apache2-mod-rewrite-htaccess-problem/td-p/896062

## License

TODO: Write license
