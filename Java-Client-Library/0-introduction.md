---
label: Introduction
order: 400
icon: note
tags: [guide]
---
# Introduction to Java Client Library

## Java Client Library 101
The Java Client Library offers Classes, Interfaces and Methods that enable the following capabilities in terms of integrating to the PAPSS System.
1. A participant can connect to PAPSS System using the `ConnectionFactory` Class.
2. Once a connection is established, a participant can send and receive Requests/Responses using the `RTPMessage` Class. This class encloses the actual message content along with some additional properties.
3. A participant is then able to call various methods to fulfill various use-cases and operations using the `EngineConnection` Interface.

The Java Client Library is composed of a set of Java classes and interfaces, the most important of which is the interface called `EngineConnection`. 
The interface has methods used for sending and receiving messages. 
Most of the operations performed in PAPSS use the `RTPMessage` class to enclose the actual message content along with some additional properties. 

---

### Sending Messages
The Participant's application that implements the Java Client Library initiates permanent requests **_(This is a necessity for detecting the online status of the Participant)_** to the PAPSS System and awaits a response from it. 
The Participant's application must await the `RTPMessage` response longer than the timeout parameter set by the payment schema - `Timeout Deadline`.  **_(For now, the parameter is 20 seconds. This value can be adjusted depending on the timeout parameter established by the SCT Inst schema)_**
This response period can be configured by Participants through the Java Client Library.

---

### Resending Messages
Resending a message by the Participant's application without receiving a reply from the PAPSS System must be executed explicitly by the Participant's application that implements the Java Client Library, without being included in the transmission protocol.

---

### Receiving Messages
In order to receive messages, Participant's application that implements the Java Client Library must use the `getMessage()` method of the `EngineConnection` Interface. 
The `getMessage()` method must be wrapped around an HTTP Long-Polling method, through which the Participant's application initiates a receive request from the PAPSS System. 
If there is an available message in the PAPSS System, this will be immediately delivered and the Participant's application initiates a new `getMessage()` request for the next message in the shortest time period. 
If there is no available message in the PAPSS System, the PAPSS System delays the zero value reply to the requesting Participant for a maximum 5 seconds.

---

## Operations
All Operations through the Java Client Library that can be performed to the PAPSS System use the XML message format from the ISO 200022 standard.

- Credit Transfer (pacs.008.001)
- Credit Transfer Return (pacs.004)
- Recall Message (camt.056.007)
- Negative Answer to Recall (camt.029.001)
- Request to Pay (pain.013.001)
  - Request to Pay Response (pain.014.001)
- Investigation (pacs.028.001)
- Identification Modification Advice (acmt.022.001)
- Identification Verification Request (acmt.023.001)
- Identification Verification Report (acmt.024.001)
- Modification Message (camt.007.002)
- Net Position Information (position.001.xsd)
- Settlement Recon (rcon.001.xsd)
- Participant Status
- GetEscrow Transaction
- GetFXRate