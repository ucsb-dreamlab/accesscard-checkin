# UCSB Access Card Reader and Check-in for DREAMLab

Users of the DREAMLab should be able to check-in and out of the lab space by
scanning their UCSB access card. This repository includes code, design plans, and
other resources related to the project of building and managing this system.

## Design overview

We're still working on this, but here is a rough idea of how the check-in system
might work.

### Reading Access Cards

A Raspberry Pi Pico with an RFID card reader (`RC522`) can be used to read the
unique identifier (uid) from a visitor's access card. A host PC (or Raspberry Pi 3/4)
can connect to the Pico and read the uid using a serial interface. 

## User Interface

The use interface will likely run in a web browser on the host computer (a PC or
Raspberry Pi) that the Pico is connected to. The webpage running in the browser
can be served by an application running on host computer. This will allow the
application to read access card uids and handle interaction from the web ui.

Visitors should be presented with two options: "Check-in" and "Check-out". To
check-in, visitors choose the appropriate option and scan their access card. If
they haven't checked-in before, a follow-up screen presents a form for entering
additional information (status, major, etc). To checkout, visitors choose
"Check-out" and scan their access card.

The application needs to be able to query and create entries in a database
(either locally or by interacting with another application) as follows:

- Get visitor info using access card uid
- Create new visitor (uid, status, major)
- Create Access Event: timestamp, checkin/out flag, card uid.
