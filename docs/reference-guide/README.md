# RFID reader-to-library integration

## How information moves

A tag identifies a library item when it enters the reader antenna field. The reader passes the read information to the host through its device interface; host software then connects the identifier with the library item record. Reading a tag and completing a library transaction are separate events: the application must resolve the identifier and confirm the requested operation.

The source presentation describes an ISO 15693 library example at 13.56 MHz with an RS-232 host interface. It mentions SIP/API integration alongside STX/ETX device framing. These occupy different interface boundaries: serial framing transports device messages, while a library-facing protocol connects circulation software. They should not be presented as interchangeable protocols.

## Responsibilities and exception handling

| Boundary | Engineering responsibility | Useful verification |
|---|---|---|
| Tag to antenna | Obtain a usable item identifier | Repeat reads with different positions and stacked items |
| Reader to host | Parse complete device messages | Inspect serial settings and framing errors |
| Host to item record | Resolve the correct library item | Check unknown and duplicate identifiers |
| Circulation transaction | Confirm the requested operation | Verify rejection and interrupted transactions |
| Security state | Keep security and loan status consistent | Check failed writes and repeat reads |

This checklist explains integration concerns rather than reporting additional completed tests. Reader dimensions and supply specifications in the reference describe its example device, not every RFID reader. Vendor illustrations remain reference material; the new diagram is an independently drawn explanation.

![Functional system explanation](system-boundaries.png)

## Reference and reuse note

Consulted local reference: **RFID.pptx — radio-frequency identification system; credited to Mohammed Anwar Almadhji, supervised by Dr. Abdulsalam Alkholidi.**

This guide uses original wording and a newly drawn diagram to explain relevant engineering ideas. The reference document and its photographs are not republished here. Source authors retain their attribution. Project implementation evidence and existing measured results remain in the main repository documentation.
