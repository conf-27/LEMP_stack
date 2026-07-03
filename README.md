# LEMP_stack
Stack LEMP testato su Rocky Linux 10.2

```bash
sudo dnf update
sudo dnf install -y php php-cli php-fpm php-mysqlnd php-gd php-mbstring php-xml php-curl php-zip php-opcache php-bcmath php-intl php-soap
sudo systemctl enable --now php-fpm.service
sudo vim /etc/php-fpm.d/www.conf
sudo dnf install -y nginx
sudo systemctl enable --now nginx
sudo vim /etc/nginx/conf.d/default.conf
sudo systemctl restart nginx.service
sudo chown -R nginx:nginx /var/lib/php
sudo vim /usr/share/nginx/html/info.php
sudo semanage fcontext -a -t httpd_sys_content_t "/var/www/html(/.*)?"
sudo firewall-cmd --add-service=http
sudo firewall-cmd --add-service=https
sudo firewall-cmd --runtime-to-permanent
sudo firewall-cmd --reload
sudo setsebool -P httpd_can_network_connect on
sudo chown -R nginx:nginx /var/www/html/
sudo chmod 755 /var/www/html/info.php
sudo restorecon -Rv /var/www/html
sudo dnf install mariadb-server
sudo systemctl enable --now mariadb
sudo mysql_secure_installation
curl -O https://wordpress.org/latest.tar.gz
sudo curl -O https://wordpress.org/latest.tar.gz
sudo tar -xzf latest.tar.gz
sudo mv wordpress html
sudo cp wp-config-sample.php wp-config.php
sudo mv /var/www/html/wordpress/* /var/www/html/
```
