# ReadyNAS Devloopment

https://github.com/ReadyNAS/sdk/wiki

Basic Structure:
`/apps` is a symlink to `/{volume}/.apps/` (first data volume). This is the home of the entire application.

**You MUST NOT create directories other than` /apps/[AppName]`.**

* `/apps/[AppName]/`
    - `web/` [Folder for web resources]
    - `config.xml` [Configuration information]
    - `https.conf` [Optional]
    - `http.conf` [Optional]
    - `fvapp-[AppName].service` [Optional: If you have your own service]
    - `logo.png` [Required]

_Hosting on our Apache server:_

* `https.conf`: If you want to host your web content on our Apache server via HTTPS, this file needs to be included. A symbolic link to this file is included from `/etc/frontview/apache/apps-https.conf`.

    - **Note:** Your web content is needs to reside in the `web/` folder.

* `http.conf`: If you want to host your web content on our Apache server via HTTP, this file needs to be included. A symbolic link to this file is included from `/etc/apache2/sites-enabled/`. You have the option to use the `web/` folder or create your own folder for storing your web content.

* A sample of both `https.conf` and `http.conf` are provided.

* You can include either `https.conf`, `http.conf`, both, or none if you wish to host from your own web server.

* A symbolic link is created from `/lib/system/system/` to `fvapp-[AppName].service`, if it exists.
* `logo.png` is required. Do not rename it. After installation, it will be accessible from `https://[NAS]/apps/logo/[AppName].png`. The logo will be presented in a 150px x 150px container, so it is recommended to create 150px x 150px PNG file.
    - Rule: `logo.png` must be 150px x 150px.


# OS 6.1.4 apache2 mod_rewrite .htaccess problem

https://community.netgear.com/t5/Using-your-ReadyNAS/OS-6-1-4-apache2-mod-rewrite-htaccess-problem/td-p/896062


## **Apache Config**

Apache config will be generated when you start Apache by systemd. You need to add `systemctl restart apache2.service` in your `postinst` file.

Depending on whether `web`, `http.conf`, and `https.conf` exist, Apache will be configured as below.

Some alias are created as below.

**url path	**  | **file system path**  | **Note**
--|---|--
  [https://nas/apps/[AppName]](https://nas/apps/[AppName])|/apps/[AppName]/web	   | If `web` folder exists.
  [https://nas/apps/logo/[AppName].png](https://nas/apps/logo/[AppName].png)|/apps/[AppName]/logo.png | If `logo.png` file exists.
