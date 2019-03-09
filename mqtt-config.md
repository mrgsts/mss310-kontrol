## Creating the Certification Authority Certificate

**Important
For the MQTT client of the MSS310 connect correctly to our MQTT server the certificates need to have some requisites, 
verify that the Common Name of your CA certificate are distict of the server cert, and ensure that the CN of the server certificate are the IP address**


- First create the private key file for the CA

```
openssl genrsa -out ca.key 2048
```

- Create a Cert Sign Request using the private key, provide the required info about CN, FQDN, Email, etc

```
openssl req -new -key ca.key -out ca.csr
```

- Using the two files we can now sign the Certificate for the CA and create the Root CA cert file ca.crt

```
openssl x509 -req -days 365 -sha1 -extensions v3_ca -signkey ca.key -in ca.csr -out ca.crt
```

Notes: we have configured 365 days of expiration


## Creating the MQTT Server certificate


- As equal that with the CA cert we need to create the key file first

```
openssl genrsa -out server.key 2048
```

- Generate the server sign request and provide the required data

```
openssl req -new -key server.key -out server.csr
```

- Sign the server.csr file with our CA certificate

```
openssl x509 -req -days 365 -sha1 -extensions v3_req -CA ca.crt -CAkey ca.key -CAcreateserial -in server.csr -out server.crt
```


Put the certificate files in the mosquitto config directory of your installation
ca.crt
server.crt
server.key

- mqtt.config
```
tls_version tlsv1
allow_anonymous true
require_certificate false
use_identity_as_username false

# by default error, information, notice and warning events are logged
#log_type error
#log_type warning
#log_type notice
#log_type information
#log_type all

# Plain MQTT protocol
listener 1883
# End of plain MQTT configuration

# MQTT over TLS/SSL
listener 8883
cafile /etc/mosquitto/ca.crt
certfile /etc/mosquitto/server.crt
keyfile /etc/mosquitto/server.key
# End of MQTT over TLS/SLL configuration
```

Enable, restart and observe the service logs to ensure the service are online

```
systemctl restart mosquitto
systemctl status mosquitto
tail -f /var/log/mosquitto/mosquitto.log
```
