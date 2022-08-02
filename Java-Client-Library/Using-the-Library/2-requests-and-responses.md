---
order: 200
icon: note
tags: [guide]
---
# Requests & Responses with `RTPMessage` Class

---
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