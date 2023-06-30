guide for  install the LOMP stack (OpenLiteSpeed, MySQL, and PHP) on Debian:


1. Update System Packages: Log in to your Debian server and update the system packages to their latest versions by running the following commands:
   ```
   sudo apt update
   sudo apt upgrade
   ```

2. Install MySQL: Install the MySQL database server by running the following command:
   ```
   sudo apt install mysql-server
   ```

3. During the installation, you will be prompted to set a password for the MySQL root user. Choose a strong password and remember it for future use.

4. Secure MySQL Installation (Optional): It is recommended to run a security script that comes with MySQL to improve the security of your installation. Run the following command and follow the instructions:
   ```
   sudo mysql_secure_installation
   ```

5. Install OpenLiteSpeed: OpenLiteSpeed is a lightweight and high-performance web server. Install it by adding the OpenLiteSpeed repository and installing the package with the following commands:
   ```
   wget -O - http://rpms.litespeedtech.com/debian/enable_lst_debain_repo.sh | sudo bash
   sudo apt update
   sudo apt install openlitespeed
   ```

6. Start OpenLiteSpeed: After the installation is complete, start the OpenLiteSpeed service using the following command:
   ```
   sudo systemctl start lsws
   ```

7. Verify OpenLiteSpeed Installation: Open a web browser and enter your server's IP address. You should see the OpenLiteSpeed administration page.

8. Install PHP: Install PHP and required modules for OpenLiteSpeed by running the following command:
   ```
   sudo apt install lsphp74 lsphp74-common lsphp74-curl lsphp74-mysql lsphp74-json lsphp74-imap lsphp74-memcached lsphp74-imagick lsphp74-gd lsphp74-mbstring lsphp74-zip lsphp74-xml lsphp74-soap
   ```

9. Configure OpenLiteSpeed for PHP: Open the OpenLiteSpeed administration page by entering your server's IP address followed by ":7080" in your web browser. Navigate to "WebAdmin console" and log in with the username "admin" and the password you set during installation.

10. Go to "Configuration" -> "Server" -> "General" and set the "Use Server Level Config File" option to "Yes". Save the changes.

11. Navigate to "Configuration" -> "Server" -> "Script Handlers" and click the "Add" button. Set the following values:
   - Name: lsphp
   - Type: LiteSpeed SAPI
   - Address: uds://tmp/lshttpd/lsphp.sock
   - Notes: LSAPI

12. Save the changes and go to "Configuration" -> "External App" -> "Add". Set the following values:
   - Name: lsphp
   - Address: uds://tmp/lshttpd/lsphp.sock
   - Max Connections: 35
   - Environment: PHP_LSAPI_MAX_REQUESTS=500

13. Save the changes and go to "Configuration" -> "Virtual Hosts" -> "Add". Configure your virtual host settings and make sure the "Enable Scripts" option is set to "Yes".

14. Test PHP: Create a PHP file in your document root directory to test PHP execution. For example, create a file named `info.php` with the following content:
   ```php
   <?php
   phpinfo();
   ?>
   ```

15. Save the file and access it in your web browser by entering your server's IP address followed by `/info.php

- You should see the PHP information page if PHP is working correctly.
