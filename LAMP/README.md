 ## Manual workflow

Install required tools

```bash
# Install Apache
sudo dnf install httpd -y # Fedora
sudo apt install apache2 -y # Debian

# Install MySQL (or MariaDB)
sudo dnf install mariadb-server -y

# Install PHP and common modules
sudo dnf install php php-mysql php-fpm -y

# Start services
sudo systemctl start httpd
sudo systemctl start mariadb
sudo systemctl start php-fpm

# Enable services to start on boot
sudo systemctl enable httpd
sudo systemctl enable mariadb
sudo systemctl enable php-fpm
```


Test file `test.php`

```bash
echo "<?php phpinfo(); ?>" | sudo tee /var/www/html/test.php
```

Then visit `http://localhost/test.php` in your browser.



