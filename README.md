# How-to-Add-trusted-root-certificates
How-to: Adding trusted root certificates to the SO (Win / MAC / Unix)

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

## Linux Ubuntu, Debian

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

## Linux CentOs 6

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

## Linux (CentOs 5)

### Add
Append your trusted certificate to file /etc/pki/tls/certs/ca-bundle.crt
```
cat foo.crt >> /etc/pki/tls/certs/ca-bundle.crt
```
