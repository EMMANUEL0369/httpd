# Readme
## Instalación
Para instalar apache2 en debian se utiliza el comando

`apt-get install apache2`.

*Se necesita permisos de root*

## Configuración
### /etc/hosts
Se agrega la siguiente linea en ipv4

`127.0.0.1       www.paginaPersonal.unam.mx`

### personal.conf
En el archivo de localizacion `/etc/apache2/sites-available` se configurara algo similar a esto 


    <VirtualHost *:80>
        # The ServerName directive sets the request scheme, hostname and port that
        # the server uses to identify itself. This is used when creating
        # redirection URLs. In the context of virtual hosts, the ServerName
        # specifies what hostname must appear in the request's Host: header to
        # match this virtual host. For the default virtual host (this file) this
        # value is not decisive as it is used as a last resort host regardless.
        # However, you must set it for any further virtual host explicitly.
        ServerName www.paginapersonal.unam.mx

        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/personal
        ErrorDocument 500 /error500.html
        ErrorDocument 403 /error403.html
        ErrorDocument 404 /error404.html
        ErrorDocument 503 /error503.html
        ErrorDocument 504 /error504.html
        <Directory /var/www/personal>
                DirectoryIndex home.html
                AllowOverride
        </Directory>

        # Available loglevels: trace8, ..., trace1, debug, info, notice, warn,
        # error, crit, alert, emerg.
        # It is also possible to configure the loglevel for particular
        # modules, e.g.
        #LogLevel info ssl:warn

        ErrorLog ${APACHE_LOG_DIR}/pagina-error.log
        CustomLog ${APACHE_LOG_DIR}/pagina-access.log combined

        # For most configuration files from conf-available/, which are
        # enabled or disabled at a global level, it is possible to
        # include a line for only one particular virtual host. For example the
        # following line enables the CGI configuration for this host only
        # after it has been globally disabled with "a2disconf".
        #Include conf-available/serve-cgi-bin.conf
    </VirtualHost>

Con el comando `a2ensite paginaPersonal.conf` se habilitara la página

*Cada cambio se tiene que reiniciar el servicio `systemctl reload apache2.service` *

### /var/www/personal

Aqui va nuestros archivos que mostraran nuestra página web
### security.conf
Por último el archivo de configuración para delimitar que informafación mostrar, asi como los encabezados. Se ubica en `/etc/apache2/conf-enabled`

`ServerTokens ProductOnly`

`ServerSignature Off`

`TraceEnable Off`

`Header set X-Content-Type-Options: "nosniff"
Header set X-Frame-Options: "sameorigin"
Header set X-XSS-Protection "1; mode=block"`
