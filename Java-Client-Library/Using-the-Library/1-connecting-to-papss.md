---
label: Connecting
order: 300
icon: note
tags: [guide]
---
# Connecting with `ConnectionFactory` Class

---

The `ConnectionFactory` class offers a set of static methods that allow getting concrete instances that implement the `EngineConnection` interface.

`GetEngineConnection` Method
```java
public static EngineConnection getEngineConnection(String channelName, String sslKeyAlias);
```

#### Input parameters:
1. Communication channel’s identifier that must be the Participant’s BIC.
2. Name (alias) of the SSL private key used by the Participant to authenticate the central RTP system. The public certificate associated to this key must be uploaded into the PAPSS System.

#### Configuration parameters:
- `HTTP_CONNECTION_TIMEOUT` – the maximum allowed time (seconds) for establishing a connection to the central RTP system. If the client library cannot establish the TCP connection for any call of a function of the central RTP system interface, then an exception of type java.net.ConnectException is raised.

#### Result: 
instance that implements the `EngineConnection` interface.

#### Exceptions: 
In case of library configuration or integration error, the method will raise an exception of type `RuntimeException`.