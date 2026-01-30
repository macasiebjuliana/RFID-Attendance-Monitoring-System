# RFID-Attendance-Monitoring-System
A QR-Barcode-based system is an input device that read printed barcodes using light rays and converts them digitally..

**1. Library & Variable Definitions**
At the very top, the code imports the tools it needs to "talk" to the hardware.
**SPI & MFRC522:** These handle the RFID card reader.
**Wire & RTClib:** These handle the Real-Time Clock (RTC) so the system knows what time it is even if it loses power.
**The Database:** You’ll see arrays like Card_UIDs[] and Student_Names[]. This acts as a mini-spreadsheet. If a card ID matches a position in the first array, it pulls the name from the same position in the second array.

**2. The setup() Function**
This runs exactly once when you plug in the Arduino.
It starts the Serial communication (to talk to your computer).
It "wakes up" the RFID reader and the Clock.
It prints a header: LABEL, Date, RFID UID... which tells a program like Excel how to organize the columns.
It gives a "Ready Beep" to let you know the system is live.

**3. The getid() and get_student_info() Helpers**
These are custom "tools" created to keep the main loop clean:
**getid():** Constantly watches the sensor. When a card is tapped, it grabs the raw "nibbles" (bits of data), converts them into a readable Hexadecimal string (like B32B7739), and returns it.
**get_student_info():** Takes that ID and searches through the arrays. If it finds a match, it packages the student's Grade, Strand, and Section into a StudentInfo structure.
These are custom "tools" created to keep the main loop clean:
**getid():** Constantly watches the sensor. When a card is tapped, it grabs the raw "nibbles" (bits of data), converts them into a readable Hexadecimal string (like B32B7739), and returns it.
**get_student_info():** Takes that ID and searches through the arrays. If it finds a match, it packages the student's Grade, Strand, and Section into a StudentInfo structure.

_Summary of Logic Flow:_
**Identify** the card.
**Retrieve** the owner's info.
**Determine** if they are arriving or leaving.
**Stamp** the time and date.
**Report** the data to the connected PC.
