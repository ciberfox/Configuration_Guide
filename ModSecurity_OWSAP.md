

# Installing and Configuring ModSecurity with OWASP Core Rule Set on Apache

ModSecurity is an open-source web application firewall that can be used to protect web applications from attacks. The OWASP Core Rule Set is a set of rules that can be used with ModSecurity to provide protection against common web application attacks.

Here's a step-by-step guide on how to install and configure ModSecurity with the OWASP Core Rule Set on Apache:

## Step 1: Install ModSecurity

The first step is to install ModSecurity on your server. You can do this using your package manager. For example, on Ubuntu, you can run the following command:

```
sudo apt-get install libapache-mod-security
```

After installing ModSecurity, you will need to enable it in Apache by running the following command:

```
sudo a2enmod security2
```

## Step 2: Install OWASP Core Rule Set

The next step is to download and install the OWASP Core Rule Set. You can do this by following these steps:

1. Go to the OWASP Core Rule Set GitHub page: https://github.com/coreruleset/coreruleset/
2. Download the latest release of the OWASP Core Rule Set (CRS).
3. Extract the contents of the CRS archive to a directory on your server.

For example, on Ubuntu, you can run the following commands:

```
wget https://github.com/coreruleset/coreruleset/releases/tag/v3.3.4
tar -xzvf v3.3.4.tar.gz
sudo mv owasp-modsecurity-crs-3.3.4 /etc/modsecurity/
```

## Step 3: Configure ModSecurity to Use the OWASP Core Rule Set

Now that you have installed both ModSecurity and the OWASP Core Rule Set, you need to configure ModSecurity to use the rules. To do this, you will need to edit the ModSecurity configuration file.

1. Open the ModSecurity configuration file in a text editor. On Ubuntu, this file is located at `/etc/modsecurity/modsecurity.conf`.
2. Find the following line in the configuration file: `SecRuleEngine DetectionOnly`
3. Change `DetectionOnly` to `On`.
4. Add the following lines to include the OWASP Core Rule Set:

   ```
   Include "/etc/modsecurity/owasp-modsecurity-crs/crs-setup.conf"
   Include "/etc/modsecurity/owasp-modsecurity-crs/rules/*.conf"
   ```

5. Save and close the file.

## Step 4: Restart Apache

The final step is to restart Apache to apply the changes you made to the ModSecurity configuration file. You can do this by running the following command:

```
sudo systemctl restart apache2
```

## Testing

Now that ModSecurity is installed and configured, you can test it by attempting to access your web application using known attack vectors. ModSecurity should block the attacks and log them to the Apache error log.

You can monitor the Apache error log using the following command:

```
sudo tail -f /var/log/apache2/error.log
```

If you see entries in the error log related to ModSecurity blocking attacks, then you know that it is working correctly. If you encounter any issues, check the error log for details on what went wrong.

Congratulations! You have successfully installed and configured ModSecurity with the OWASP Core Rule Set on Apache. Your web application is now protected against common web application attacks.
