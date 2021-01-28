# NMEA2000-Workshop

Wenn alle Vorbereitungen erfolgreich durchgeführt wurden, können wir nun starten.

## NMEA2000

NMEA2000 ist eine standardisierte Erweiterung des älteren Protokolls [NMEA0183](https://de.wikipedia.org/wiki/NMEA_0183). Grundlegende Informationen zu NMEA2000 sind [hier](https://de.wikipedia.org/wiki/NMEA_2000) zu finden.

Im Rahmen des Workshops werden wir ein kleines NMEA2000-Netzwerk aufbauen und erste Programme mit der [NMEA2000-Bibliothek](https://github.com/ttlappalainen) von Timo Lappalainen erstellen und ausprobieren.

Die üblichen Hersteller verkaufen ihre NMEA2000-/CAN-Bus-Kabel zu extremen Preisen. Eine günstigere Alternative ist das CAN-BUS-Kabel von Unitronic. Unter anderem erhältlich bei [Voelkner](https://www.voelkner.de/products/146612/LAPP-2170261-1-Busleitung-UNITRONIC-BUS-2-x-2-x-0.22mm-Violett-Meterware.html). Zum Beispiel in Verbindung mit schraubbaren [Micro-C-Steckverbindern](https://www.gmm-yacht.de/nmea_2000_installation.html).

Für kleinere Netzwerke funktionieren aber auch alle anderen paarweise verdrillten Leitungen (inclusive [CAT-5](https://www.reichelt.de/cat-5e-patchkabel-sf-utp-25m-4x2-awg26-7-25s-p505.html?&nbc=1&trstct=lsbght_sldr::2520) Ethernet-Netzwerkkabel). Gerne auch geschirmt; der [CAN-Bus-Standard](https://de.wikipedia.org/wiki/Controller_Area_Network#Maximale_%C3%9Cbertragungsrate_und_Leitungsl%C3%A4nge) fordert das aber nicht. 

Für die feuchte Bootsumgebung ist aber das Kabel allein nicht entscheidend, sondern die Qualität der Verbindungen und Stecker.

## ESP32
Wir werden im Workshop den Prozessor ESP32 von Espressif nutzen. Zur einfacheren Verwendung werden wir ein "ESP32 Dev Module" verwenden, bei dem die notwendige externe Beschaltung schon vorhanden ist. Inclusive USB-Anschluss, der für die Workshop-Beispiele auch die Spannungsversorgung liefert. Für die Beispiele auf dem Steckbrett nutzen wir das [Development-Modul](https://www.az-delivery.de/blogs/azdelivery-blog-fur-arduino-und-raspberry-pi/esp32-das-multitalent) von AzDelivery. Es hat diese [Pin-Belegung](https://www.dropbox.com/s/o90qsp1rn5ol9gf/NodeMCU.png?dl=0).

## NMEA2000 Bibliothek
Für die spätere Nutzung der NMEA2000-Bibliothek sind speziell drei Dateien wichtig:
1. NMEA2000-Library-Referenz [Link](https://github.com/ttlappalainen/NMEA2000/blob/master/Documents/NMEA2000_library_reference.pdf)
2. Header-Datei "N2kMessages.h" mit den PGN-Definitionen [Link](https://github.com/ttlappalainen/NMEA2000/blob/master/src/N2kMessages.h)
3. Header-Datei "N2kTypes.h" mit Definitonen für Datentypen in den PGNs [Link](https://github.com/ttlappalainen/NMEA2000/blob/master/src/N2kTypes.h)

## Download des Repositories
Der einfachste Weg, die Beispielprogramme zu nutzen, ist das ganze NMEA2000-Workshop-Repository als ZIP-Datei herunterzuladen. Dazu klickt man oben auf "NMEA2000-Workshop" und dann auf den grünen Button "Code". Dann "Download ZIP" auswählen. Die heruntergeladene ZIP-Datei in einen frei wählbaren Ordner entpacken. 

Dann kann man die Beispielprogramme direkt in der Arduino-IDE öffnen. Dazu einfach auf die jeweilige .ino-Datei doppelklicken. Alle Programme befinden sich im Ordner "Software".

Eine HTML-Version des Workshops befindet sich im Ordner "HTML". Damit kann der Workshop auch Offline, ohne GitHub genutzt werden. Zum Start einfach "Start.html" anklicken.

## Vorbereiten des linken ESP32
Auf dem **linken** ESP32 ist der Sketch [ActisenseListenerSender-ESP32.ino](https://github.com/AK-Homberger/NMEA2000-Workshop/blob/main/Software/ActisenseListenerSender-ESP32/ActisenseListenerSender-ESP32.ino) zu installieren. Dazu im entpackten ZIP-Ordner die Datei "ActisenseListenerSender-ESP32.ino" doppelklicken. Die Arduino-IDE startet dann mit geladenem Sketch. Dann nur den linken ESP32 mit USB verbinden und in der Arduino-IDE den seriellen USB-Port auswählen und "Sketch" "Hochladen" anwählen. **Den seriellen Port bitte notieren**.

Im unteren Statusfenster wird beim Übertragen "Connecting........_____....._____.." angezeigt. Normalerweise erfolgt das Hochladen nach ein paar Sekunden automatisch. Falls die Fehlermeldung "A fatal error occurred: Failed to connect to ESP32:" angezeigt wird, kann es helfen, während des Upload-Prozesses, die "Boot"-Taste auf dem ESP2-Board gedrückt zu halten, bis der Upload-Prozess startet.

Sobald "Leaving...  Hard resetting via RTS pin..." angezeigt wird, ist das Programm erfolgreich übertragen und auch schon gestartet worden.

## Workshop-Beispielprogramme
Auf dem rechten ESP32 werden unterschiedliche Programme installiert, um die Nutzung der NMEA2000-Bibliothek zu erklären. Dazu wird der ESP32 mit USB verbunden und in der Arduino-IDE der neue serielle USB-Port ausgewählt.

Mit dem NMEA-Reader können wir Daten vom NMEA2000-Netzwerk anzeigen, und mit dem NMEA-Simulator auch Daten an das Netzwerk senden. Beides werden wir im Workshop nutzen.

Folgende Beispielprogramme werden im Workshop gemeinsam erstellt/erweitert und mit dem Reader/Simulator getestet:

1. [NMEA2000-Thermometer, Hygrometer und Barometer mit BME280 (I2C)](https://github.com/AK-Homberger/NMEA-Workshop/blob/main/Docs/BME280.md)
2. [Temperaturfühler mit DS18B20 (1-Wire)](https://github.com/AK-Homberger/NMEA-Workshop/blob/main/Docs/DS18B20.md)
3. [Spannungs- und Widerstandsmessung (Batteriespannung, Tankanzeige)](https://github.com/AK-Homberger/NMEA2000-Workshop/blob/main/Docs/AnalogRead.md)
4. [Messung von Frequenzen (ESP32-Interrupts nutzen)](https://github.com/AK-Homberger/NMEA2000-Workshop/blob/main/Docs/Frequenz.md)
5. [Daten (PGNs) vom NMEA-2000-Bus lesen und darstellen](https://github.com/AK-Homberger/NMEA2000-Workshop/blob/main/Docs/ReadPGNs.md)
6. [NMEA2000-WLAN-Gateway und Anzeige der Daten auf OpenCPN und Tablet/Telefon](https://github.com/AK-Homberger/NMEA2000-Workshop/blob/main/Docs/WLAN-GW.md)
7. [Gateway plus AIS-Multiplexing](https://github.com/AK-Homberger/NMEA2000-Workshop/blob/main/Docs/WLAN-GW3.md)
8. [Optional: Gateway mit Web-Server](https://github.com/AK-Homberger/NMEA2000-Workshop/blob/main/Docs/WLAN-GW4.md)

