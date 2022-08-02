---
order: 300
icon: note
tags: [guide]
---
# Connecting with `ConnectionFactory` Class

---

## RTPMessage Class

The `RTPMessage` Class contains the following fields:

- `Type: String` – it represents the type of reply message that the central RTP sends. Its possible values are: 
  - `camt.029`, 
  - `camt.056`, 
  - `pacs.008`, 
  - `pacs.004`, 
  - `pacs.002`, 
  - `pacs.028`, 
  - `recon.001`
- `Sequence: long` – sequence of the message received by Participant from the central RTP system. This sequence is assigned by the system when messages are generated. 
- `Content: String` – XML content of the received/sent message from/to the central RTP system.
- `ErrorCode: integer` – the internal error code reported by the system for the sent message. Please see details in section 7.2.
- `ReportedStatus: String` – ACCP or RJCT code for a pacs.002 type message received from the central system.
- `ProcessingDuration: long` – total processing time of a message send to the central system, expressed in nanoseconds.
---


## `EngineConnection` Interface
---
### SendNewMessage

```java
RTPMessage sendNewMessage(RTPMessage message) throws IOException;
```
This method is used for sending new messages. All PAPSS message types are supported by this method except `pacs.002`.

---


### ReplyToPayment
```java
RTPMessage replyToPayment(RTPMessage message) throws IOException;
```
This method is used by receiver Participants to reply positively or negatively to a payment message received from PAPSS

---

### GetMessage
```java
RTPMessage getMessage() throws IOException;
```
This method serves 2 purposes. 
1. to receive incoming messages for a Participant from PAPSS.
2. to register the ONLINE status of a Participant. All participants must register themselves as being ONLINE every 5 seconds with PAPSS.

In the first case, If there is no available message for the Participant, the method replies with a value of `null`. 
In both cases, weather calling this function returns a message or not, the Participant must initiate a new call immediately (within maxim 5 seconds), to keep the ONLINE status of Participants and check availability of pacs.008 messages.

---

### ConfirmMessage
```java
void confirmMessage(long sequence) throws IOException;
```
The method is used by a Participant to confirm receiving a message. 
A message received from PAPSS must be confirmed explicitly by the Participant by using this method. 
If the confirmation is executed after a period of time larger than PAPSS' Output Redelivery Time `(5 seconds)`, 
the system will automatically resend the unconfirmed messages by placing them in the message queue processed by the function `GetMessage`.

Input parameters: sequence of received message. This is to be found in the object of `RTPMessage` received as the result of `GetMessage` function’s execution.

---

### GetPositions
```java
String getPositions() throws IOException;
```
This method is used by a Participant to get the position of: the technical account, the guarantee ceiling and the available amount limit for their own account.
This method returns an XML message that contains the current values of technical accounts’ balances at the time of the call. Sample XML message returned is as below:
```xml
<?xml version="1.0" encoding="UTF-8"?> <positions xmlns="urn:montran:positions.001"> <snapshot instgAgtId="NG0002" lastTranSeq="10104" timestamp="2017-06-06T19:22:38+03:00" > <conditions conditions agtId=" NG0002 "> <condition accountCode=’NG0002-NGN-CA' ccy='NGN' condType='COMPLETE' balance='470000.00' overdraft='0.00' debitAmount='100000.00' debitCount='1' creditAmount='30000.00' creditCount='1'/> <condition accountCode=’NG0002-NGN-CA' ccy='RON' condType='HOLD' balance='0' debitAmount='0' debitCount='0' creditAmount='0' creditCount='0'/> </conditions></snapshot> </positions>
```

---


### GetIndirectPositions
```java
String getIndirectPositions() throws IOException;
```
This method is used by a settlement agent Participant to obtain the guarantee ceilings for associated non-settlement Participants.

---

### GetParticipantStatus
```java
String getParticipantStatus(ParticipantIdType idType, String id) throws IOException;
```
This method is used by any Participant to obtain the connection status of another Participant as well as the payment schema information for the respective Participant.
This method returns an XML message that contains statuses information for the required Participant.

---

### GetAllParticipantStatus
```java
String getAllParticipantsStatus(Boolean online, ParticipantType type) throws IOException;
```
This method is used by any Participant to obtain the connection status of all Participants as well as the payment schema information for each Participant on the list.

Input parameters:
1. `Boolean online` – parameter will filter the list of participants based on weather they are in ONLINE status or not at the time of this method being called.
2. `ParticipantType type` – parameter will filter the list of the participants based on their type. The list of participant types is as follows: `ADMINISTRATOR`, `CENTRL_BANK`, `BANK`, `MOBILE_NETWORK_OPERATOR`, `VIRTUAL_ACCOUNT_OPERATOR`, `CARD_OPERATOR`.

This method returns an XML message that contains statuses and payment schema information for all filtered Participants. The XML format is similar with GetParticipantStatus XML format with multiple <participant> entries.

---

### GetEscrowTransactions
```java
String getEscrowTransactions(String debtorAccount) throws IOException;
```
This method is used to obtain a list of escrow transaction which are in RESERVE status and which were originated by the caller participant.

---

### GetFXRate
```java
String getFxRate(
            String senderCurrency,
            String senderCountryCode,
            String receiverCurrency,
            String receiverCountryCode,
            String receiverBank,
            String localInstrument,
            String amount,
            boolean invoicePayment
        ) throws IOException;
```
This method is used to obtain a specific FX Rate that is currently applied between Sender Country/Currency and Receiver Country/Currency and for a specific local instrument.
This method returns an XML message that contains the necessary rates used to determine the final rate between selected currencies and the computed final rate.