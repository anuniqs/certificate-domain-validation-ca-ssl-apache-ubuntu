

### Step 1 — Generate a CSR (Certificate Signing Request)


`anup@megatron:~$ openssl req -new -newkey rsa:2048 -nodes -keyout anurish_key.key -out anurish_key.csr`
```
Country Name (2 letter code) [AU]:IN
State or Province Name (full name) [Some-State]:KA
Locality Name (eg, city) []:Bangalore
Organization Name (eg, company) [Internet Widgits Pty Ltd]:AnuRish Brand Corp.
Organizational Unit Name (eg, section) []:AnuRish IT     
Common Name (e.g. server FQDN or YOUR name) []:Anup Kumar Mondal
Email Address []:uniqs.anup@gmail.com

Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:AnuRishKey'2020
An optional company name []:AnuRish Brand Corp.   
```

**Find keys**

`anup@megatron:~$ ls -ltr`  
```
anurish_key.key  
anurish_key.csr  
```  

**What Keys Contains**

`anup@megatron:~$ cat anurish_key.key`
`anup@megatron:~$ cat anurish_key.csr`


### Step 2 — Download certificates and locate them
The Certificate Authority will email you a zip-archive with several .crt files.
The zip-archive will contain the Certificate for your domain name (.crt) and the CA-Bundle (.ca-bundle) file.

Keep these Certificactes to `/etc/ssl/certs/`

```
/etc/ssl/certs/anurish_cert.crt
/etc/ssl/certs/anurish_cert.key
/etc/ssl/certs/anurish_cert.ca-bundle
```

### Step 3 — Configure Virtual Host Section (Domain block in NGINX)
Apache server installed on the Ubuntu operating system, each site has a separate configuration that can be found at `/etc/apache2/sites-enabled/`  

`anup@megatron:~$ /etc/apache2/sites-enabled/try_domain.com.conf`

```
<VirtualHost [IP ADDRESS]:443>
	ServerAdmin uniqs.anup@gmail.com
	DocumentRoot var/www
	ServerName try_domain.com
	ErrorLog www/home/logs/error_log
	SSLEngine on
	SSLUseStapling on
	SSLCertificateFile /etc/ssl/certs/anurish_cert.crt
	SSLCertificateKeyFile /etc/ssl/certs/anurish_cert.key
	SSLCertificateChainFile /etc/ssl/certs/anurish_cert.ca-bundle
</VirtualHost> 
```
Restart apache server `sudo systemctl status apache2` and browse your domain name to varify and for details visit https://www.sslshopper.com/ssl-checker.html

<hr />

`@AnuRish Brand Corp. , +91-9620481097 , uniqs.anup@gmail.com , https://www.linkedin.com/in/anuniqs/`
