# gitweb setup abandoned for gitlist

## **Minor changes to ReadyNAS**

```sh
root@NAS01:/var/www# cp /usr/share/gitweb/gitweb.cgi  /usr/lib/cgi-bin/gitweb.cgi
```

## Tested out on Ubuntu 8.04:

[Server Fault](https://serverfault.com/questions/72732/how-to-set-up-gitweb)


`sudo apt-get install apache2 git-core gitweb`

`sudo a2enmod rewrite`

Assuming that you git projects are in /pub/git, edit the file: `/etc/gitweb.conf`

```sh
$projectroot = "/pub/git";
$git_temp = "/tmp";
#$home_link = $my_uri || "/";
$home_text = "indextext.html";
$projects_list = $projectroot;
$stylesheet = "/gitweb.css";
$logo = "/git-logo.png";
$favicon = "/git-favicon.png";
# enable human readable URLs
$feature{'pathinfo'}{'default'} = [1];

```

Now, setup a new virtual host in Apache config directory. Edit a new file called:` /etc/apache2/sites-available/gitweb`

```
<VirtualHost *>
   ServerName     git.mydomain.com
   ServerAlias    git

   DocumentRoot /pub/git
   SetEnv GITWEB_CONFIG /etc/gitweb.conf

   RewriteEngine on
   RewriteRule ^/$                                            /gitweb [PT]
   RewriteRule ^/(.*\.git/(?!/?(HEAD|info|objects|refs)).*)?$ /gitweb%{REQUEST_URI}  [L,PT]

   # Aliases
   ScriptAlias /gitweb           /usr/lib/cgi-bin/gitweb.cgi
   Alias       /gitweb.css       /usr/share/gitweb/gitweb.css
   Alias       /git-logo.png     /usr/share/gitweb/git-logo.png
   Alias       /git-favicon.png  /usr/share/gitweb/git-favicon.png

   # Logfiles
   ErrorLog  /var/log/apache2/gitweb.error.log
   CustomLog /var/log/apache2/gitweb.access.log combined
</VirtualHost>
```
Enable the new site:

`sudo a2ensite gitweb`

Restart Apache:

`sudo invoke-rc.d apache2 restart`
