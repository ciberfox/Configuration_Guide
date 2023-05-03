# Guide for Installing Apache, PHP, MySQL in Oracle Solaris

In this guide, we will be installing Apache, PHP, and MySQL in Oracle Solaris. These are some of the most commonly used tools for web development and are used by many developers worldwide. 

## Prerequisites

Before we begin the installation process, make sure that you have the following prerequisites installed:

- Oracle Solaris operating system
- Root access to the system
- Internet connectivity for downloading packages

## Installing Apache

1. Open the terminal and log in as the root user.
2. Update the package repository using the following command:

   ```
   pkg update
   ```
   
3. Install the Apache web server using the following command:

   ```
   pkg install apache-24
   ```

4. Start the Apache service using the following command:

   ```
   svcadm enable apache24
   ```

5. To verify that Apache is installed and running, open a web browser and enter the following URL:

   ```
   http://localhost/
   ```
   
   You should see the Apache test page displayed in the browser.

## Installing PHP

1. Install PHP using the following command:

   ```
   pkg install php-73
   ```

2. After installation, restart the Apache service:

   ```
   svcadm restart apache24
   ```

3. To verify that PHP is installed and working, create a PHP file with the following code:

   ```
   <?php phpinfo(); ?>
   ```

4. Save the file with the extension ".php" in the Apache web server document root directory, which is located at:

   ```
   /var/apache2/2.4/htdocs/
   ```

5. Open a web browser and enter the following URL:

   ```
   http://localhost/your_php_file.php
   ```

   You should see the PHP information page displayed in the browser.

## Installing MySQL

1. Install MySQL using the following command:

   ```
   pkg install mysql-80
   ```

2. Start the MySQL service using the following command:

   ```
   svcadm enable mysql
   ```

3. Secure the MySQL installation by running the following command:

   ```
   mysql_secure_installation
   ```

   Follow the on-screen prompts to set a root password and other security settings.

4. To verify that MySQL is installed and running, enter the following command:

   ```
   mysql -u root -p
   ```

   Enter the root password that you set during installation. If you are able to log in to the MySQL prompt, then MySQL is installed and running.
.
