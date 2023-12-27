---
title: "Creating and Installing SSL Certificates"
layout: post
---
Summary:
  1. Creating a Self-Signed Certificate
  2. Configuring the Apache SSL File
  3. Testing the SSL Certificate

To begin this exercise I launched and logged into the root account of a Kali Linux virtual machine. Following this, I opened a terminal window and generated an SSL key with the command:

  - openssl genrsa -out ca.key 2048

Then generated a new Certificate Signing Request (CSR) by entering the command:

  - openssl req -new -key ca.key -out ca.csr

Then, when prompted, I entered the Country Name, State, Locality Name, Organization Name, Organization Unit Name, Common Name, Email Address, Challenge Password, and Company Name provided to me.

Once the information was entered, I generated a self-signed key by entering the command:

  - openssl x509 -req -days 365 -in ca.csr -signkey ca.key -out ca.crt

![image](https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/82f036bc-680a-4a38-b466-2b237aceff77)

Then copied the ca.crt, ca.key, and ca.csr from their directories using cp.

Next, I began configuring the Apache SSL file by navigating to the etc/apache2/sites-available/ directory and copying the default-ssl.conf file.

Then I began to edit the localhost-ssl.conf file by entering the command:

  - mousepad localhost-ssl.conf

and changed the SSLCertificateFile and SSLCertificateKeyFile paths.

![image](https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/416782a6-7a72-4ed8-9c8f-e1083297cfdb)

Finally, I began to test the SSL Certificate by navigating to the /etc/apache2/sites-enabled/ directory and enabled the localhost-ssl site with the command:

  - ln -s /etc/apache2/sites-available/localhost-ssl.conf

and enabled the SSL Apache Mod with the command:

  - a2enmod ssl

then finally, I restarted the apache service with the command:

  - service apache2 restart

Once the service is restarted I opened a window of Mozilla Firefox and typed https://localhost into the address field and accepted the risk of the Potential Security Risk Ahead alert.

From this point, I was able to recognize that a self-signed SSL Certificate was successfully implemented and clicked on the padlock to view the certificate.

<img width="405" alt="image" src="https://github.com/Devin10Dahlberg/devin10dahlberg.github.io/assets/149525072/857b1341-c1da-4e5c-9881-fb43d92eb254">

