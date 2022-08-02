---
label: Digital Signature
order: 100
icon: git-compare
tags: [guide]
---
# Digital Signature with `XMLSignatureUtils` Class

#### Digital Signature Application and Verification

---

The Java Client library provides Participants with a set of functions for applying and verifying the digital signature of messages exchanged with the PAPSS system. 
These functions are offered by the `XMLSignatureUtils` class and are described in the next sections.

## `GenerateSignature` Method
```java
public String generateSignature(String xmlContent) throws SignatureException;
```
This method is used for applying the digital signature to an XML message before it is sent to the central RTP system. The alias of the private key used for the signature is configured in `security.properties`.

This method takes XML message in String format as input. The message structure must be according to the `montran.message.01` schema, which contains a `head:BusinessApplicationHeader` structure defined by ISO 20022, where the digital signature is to be inserted.

This method return a digitally signed XML message in String format.

Exceptions: In case of library configuration or signature entry error, the method will raise a `SignatureException`.

## `ValidateSignature` Method
```java
public void validateSignature(Document xmlContent) throws SignatureValidationException
```
This method is used for validating the digital signature to an XML message, represented as a DOM document, received from the PAPSS System. The alias of the private key used for the signature is configured in `security.properties`.

Input parameters:
• this methos takes XML message in `org.w3c.dom.Document` format. The message structure must be according to the `montran.message.01` schema, which contains a `head:BusinessApplicationHeader` structure defined by ISO 20022, where the digital signature is to be inserted.
