# desafio17
Documentacion del desafio 17
dejo tods los comando uilizados:
-Instalar PAM y configurar pam_cracklib:
-cpp
Comandos:
sudo apt-get install libpam-cracklib
sudo nano /etc/pam.d/common-password
-Añadir la línea:
cpp
password        requisite                       pam_cracklib.so retry=3 minlen=12 difok=3
password        [success=1 default=ignore]      pam_unix.so obscure use_authtok try_first_pass sha512
password        requisite                       pam_deny.so
password        required                        pam_permit.so

2.	Configuración de SSH y Google Authenticator:
-Configurar SSH para usar llaves:
-cpp
sudo nano /etc/ssh/sshd_config
-Asegurarse de que las siguientes líneas estén presentes:
-cpp
PubkeyAuthentication yes
PasswordAuthentication no
-Instalar y configurar Google Authenticator:
cpp
sudo apt-get install libpam-google-authenticator
google-authenticator
sudo nano /etc/pam.d/sshd
-Añadir la línea:
cpp
auth required pam_google_authenticator.so
	
3.Configuración de sudo y Permisos del Sistema de Archivos:
-Editar el archivo de configuración de sudo:
cpp
sudo visudo
-Añadir:
cpp
educacionit ALL=(ALL) NOPASSWD: /usr/sbin/apache2ctl, /usr/bin/systemctl restart mariadb, /usr/bin/systemctl start mariadb, /usr/bin/systemctl reload mariadb, /usr/bin/systemctl status mariadb
-Ajustar permisos del sistema de archivos:
cpp
sudo chown -R root:root /var/www
sudo chmod -R 755 /var/www	
4.Configuración de Apache2:
-Editar el archivo de configuración de Apache2:
cpp
sudo nano /etc/apache2/apache2.conf
-Asegurarse de que los permisos sean adecuados:
cpp
<Directory /var/www/>
    Options Indexes FollowSymLinks
    AllowOverride None
    Require all granted
</Directory>
Check (Verificar)

