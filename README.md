# How-to-Add-trusted-root-certificates
How-to: Adding trusted root certificates to the SO (Win / MAC / Unix).
###### Feel totally free to edit this page to add another operating systems!

##### How-to list all available ssl CA certificates in Linux.
```
# Arch , Debian, Ubuntu
awk -v cmd='openssl x509 -noout -subject' ' /BEGIN/{close(cmd)};{print | cmd}' < /etc/ssl/certs/ca-certificates.crt

# Red-Hat, Fedora, CentOS
awk -v cmd='openssl x509 -noout -subject' ' /BEGIN/{close(cmd)};{print | cmd}' < /etc/ssl/certs/ca-bundle.crt

# Centos 5
awk -v cmd='openssl x509 -noout -subject' ' /BEGIN/{close(cmd)};{print | cmd}' < /etc/pki/tls/certs/ca-bundle.crt
```
---

## Mac OS X

### Add
```
sudo security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.keychain ~/new-root-certificate.crt
```
### Remove
```
sudo security delete-certificate -c "<name of existing certificate>"
```

---

## Windows

### Add
```
certutil -addstore -f "ROOT" new-root-certificate.crt
```

### Remove
```
certutil -delstore "ROOT" serial-number-hex
```

---

## Ubuntu, Debian, Arch

### Add
Copy your CA to dir /usr/local/share/ca-certificates/
```
sudo cp foo.crt /usr/local/share/ca-certificates/foo.crt
```
Update the CA store:
```
sudo update-ca-certificates
```

### Remove

Remove your CA (/usr/local/share/ca-certificates/)
```
sudo update-ca-certificates --fresh
```

---

## Suse 

### Add
Copy your CA to dir /etc/pki/trust/anchors/
```
sudo cp foo.crt /etc/pki/trust/anchors/foo.crt
```
Update the CA store:
```
sudo update-ca-certificates
```

---

## CentOs > 6.X

### Add
Install the ca-certificates package:
```
yum install ca-certificates
```
Enable the dynamic CA configuration feature:
```
update-ca-trust force-enable
```
Add it as a new file to /etc/pki/ca-trust/source/anchors/:
```
cp foo.crt /etc/pki/ca-trust/source/anchors/
update-ca-trust extract
```

---

## CentOs < 5.X

### Add
Append your trusted certificate to file /etc/pki/tls/certs/ca-bundle.crt
```
cat foo.crt >> /etc/pki/tls/certs/ca-bundle.crt
```

---

## Firefox Browser
Firefox has its own certificate store.
```
Firefox Options -> Advanced -> Certificates
```

---

## Links of interest​ (Acrobat, Android, etc)
How can I trust CAcert's root certificate?: http://wiki.cacert.org/FAQ/ImportRootCert
