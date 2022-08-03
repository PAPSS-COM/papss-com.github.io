---
order: 300
icon: gear
tags: [guide]
---
# Configuration

---

There are 2 important files for configuring the Java Client Library in the Participant's application.
1. `client-config.properties` - for configuration of client parameters needed by the Java Client Library to communicate with PAPSS System.
2. `security.properties` - for configuration of keystore files and certificates used by the Participant's application.

These 2 properties configuration files must be present in the Participant's application's classpath.
Ideally in a Springboot application this will be in the /resources folder.

---

## ClientConfig Configuration
#### `client-config.properties`

The configurable parameters for `client-config.properties` are presented in the table below:

| Name     | Value Example                             | Description                                                                                                                            |
|----------|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| BASE_URL | BASE_URL=https://sandbox.api.xxx.papss.io | URL address of PAPSS System.                                                                                                           |
| MY_DNSxxx | MY_DNSpapss.org=10.1.1.1,10.1.1.2         | Local translation of the IP address (in the library).                                                                                  |
| HTTP_CONNECTION_TIMEOUT | HTTP_CONNECTION_TIMEOUT=2                 | Maximum allowed time (seconds) for establishing a connection to the PAPSS System.                                                      |
| HTTP_SEND_MESSAGE_TIMEOUT | HTTP_SEND_MESSAGE_TIMEOUT=25              | Maximum allowed time (seconds) for sending a message. It must be larger than the maximum allowed time according to the payment schema. |
| HTTP_RECEIVE_MESSAGE_TIMEOUT | HTTP_RECEIVE_MESSAGE_TIMEOUT=10           | Maximum allowed time (seconds) for receiving a message from the central system.                                                        |
| SIGN_OUTGOING | SIGN_OUTGOING=true                        | Boolean to sign out going messages                                                                                                     |

---
## Security Configuration
#### `security.properties`

The configurable parameters for `security.properties` are presented in the table below:

| Name     |  Description                                                                                                                            |
|----------|-------------------------------------------|
| keyPass | password for all configured keystore files. |
| SSLkeyFile | path to the keystore that holds the own SSL type certificate (client) for the authentication to the central RTP system. The client library will use the private key certificate from the keystore certificate suggested by the sslKeyAlias parameter when a connection was created. |
| SSLtruststore | path to the keystore that holds public certificates of servers and of server certificate issuer entities to which the RTP system connects. It is used by the Customer application to authenticate the central RTP system. |
| DSkeyFile | path to the keystore that holds the own Digital Signature certificate used for the signature of messages sent to the RTP. The certificate used by the application is indicated by the keyAlias parameter. |
| DSTruststore | path to the keystore that holds the servers’ public certificate or certificates of server certificate issuer entitites to which the RTP application connects. It is used by the Customer application for the verification of the digital signature of messages sent by the central RTP system. |
| keyAlias | private key alias used for the digital signature. |









---



