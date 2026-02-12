# TriMod 2.0 Adapter

![](https://codeberg.org/diwou/TriMod_2.0_Adapter/raw/branch/main/Images/TriMod_Adapter_2.0.jpg)


## Einleitung

Mit Hilfe dieses Adapters kann ein Commodore 1541 Floppy-Laufwerk in ein Commodore 2031LP umgewandelt werden. Der Unterschied zwischen den beiden Laufwerken liegt in der Schnittstelle zur Außenwelt.

Während die 1541 mit dem CBM-Bus zum Anschluss an den Commodore C64 & C128 ausgestattet war, kann die 2031LP an die "großen" Computer von Commodore der PET- und CBM-Serie angeschlossen werden. Zu diesem Zweck verfügt dieses Laufwerk über eine parallele IEEE-488 (auch bekannt als GPIB) Schnittstelle.

Die Idee, eine Commodore 1541 in eine 2031LP umzuwandeln, stammt ursprünglich von André Fachat. Es gab dazu auch Anleitungen für einen entsprechenden Adapter in den 80er Jahren in der deutschen Computerzeitschrift "64'er".

Ich habe diese Idee weiterentwickelt und so entstand der TriMod-Adapter.

Das Besondere daran ist, dass er nicht nur umschaltbar ist, sondern auch ein Parallelkabel für Floppy-Speeder wie SpeedDOS bereitstellt.

Die erste Version des TriMod-Adapters war noch diskret mit TTL-Bausteinen aufgebaut und konnte "nur" zwischen dem CBM-Bus und IEEE-488 umschalten.

Mit dem TriMod-Adapter 2.0 habe ich die TTL-Komponenten durch ein CPLD ersetzt sowie die Möglichkeit geschaffen, SpeedDOS usw. wieder zu verwenden.

Soweit mir bekannt ist, war der TriMod Adapter 2.0 nicht nur der erste funktionierende Adapter auf CPLD-Basis, sondern auch der erste, der einen Parallelkabelanschluss für Floppy-Speeder bot.

![](https://codeberg.org/diwou/TriMod_2.0_Adapter/raw/branch/main/Images/TriMod_Adapter_2.0_complete_view.jpg)

![](https://codeberg.org/diwou/TriMod_2.0_Adapter/raw/branch/main/Images/TriMod_Adapter_2.0_top_view.jpg)


## Hintergrundinformationen

Anfang 2019 hatte ich eine Nachbildung der Hauptplatine des Commodore Floppy 1541 erstellt. Ich hatte einige Laufwerke, bei denen die Platine nicht mehr in gutem Zustand war, teilweise Haarrisse und viele Leiterbahnen mussten von Hand repariert werden.

Also habe ich mich hingesetzt, viele Schaltpläne durchforstet (leider gibt es keinen einzigen korrekten Schaltplan ohne Fehler) und viele Verbindungen durchgemessen. So entstand im Frühjahr 2019 die erste Version.

Gleichzeitig entwickelte ich meinen ersten TriMod-Adapter. Irgendwann kam mir die Idee, das Ganze zu kombinieren.

Ich hatte nun einen funktionierenden Schaltplan der 1541 in elektronischer Form. Also entschied ich mich, die Platine der 1541 etwas zu "pimpen".

Im Laufe der Entwicklung stellte ich dann fest, dass die Platine natürlich immer größer wurde. Nicht, dass in der 1541 nicht genug Platz gewesen wäre, aber der Preis für die Herstellung stieg immer weiter.

Also kam der Gedanke, das Ganze in ein CPLD zu packen.

Damit ich bei Fehlern nicht immer eine große Hauptplatine machen musste, entwickelte ich zuerst einen Adapter, der in eine 1541 eingesteckt werden kann.

So entstand im Herbst 2019 der erste TriMod 2.0 Adapter.

![](https://codeberg.org/diwou/TriMod_2.0_Adapter/raw/branch/main/Images/TriMod_Adapter_CPLD_Version.jpg)

Dieser Adapter war daher nie für etwas anderes gedacht, als eine neue Systemplatine für die 1541 zu entwickeln. Daher habe ich nicht darauf geachtet, dass er besonders klein ist, gut in die 1541 passt oder das Gehäuse schließbar ist.

Nachdem ich die Dateien für den ersten Adapter auf GitHub veröffentlicht hatte, erhielt ich viele Anfragen, eine kleinere Version zu veröffentlichen.

Mit diesem Adapter möchte ich diesem Wunsch nachkommen.


## Technische Informationen

Aufgrund der vielen benötigten I/Os wurde ein größeres CPLD in Form des Xilinx XC95144XL-10TQ100 benötigt. Leider ist dieses TQFP-100-Gehäuse so groß, dass es nicht mehr zwischen eine DIP-40-Fassung passt. Zusätzlich werden die beiden Treiberbausteine SN75160 und SN75161 benötigt, die selbst in SMD nicht gerade winzig sind.

Und leider sind diese beiden Komponenten zu groß, um unter eine DIP-40-Fassung zu passen.

Außerdem wollte ich keine SMD-Stiftleisten verwenden, da viele Leute Probleme beim Löten haben. Zudem finde ich diese auch in der Version mit gedrehten Präzisionskontakten recht teuer.

Ich habe daher alles so kompakt wie möglich gehalten und die Komponenten sehr dicht beieinander platziert.

Dann habe ich die Standard-IDC-Header durch MicroMatch-Steckverbinder ersetzt. Diese sind etwas kleiner, verwenden aber dasselbe Flachbandkabel.

Und so entstand der neue TriMod 2.0 Adapter.


## Funktionen

- 3 Schnittstellen: CBM-Bus, Anschluss für Parallelkabel und IEEE-488
- Umschaltbar zwischen CBM-Bus (inkl. Parallelkabel) und IEEE-488
- Gleiche Geräte-ID in beiden Modi
- Beim Umschalten oder Ändern der Geräte-ID wird die Floppy automatisch zurückgesetzt
- Wenn die Floppy im IEEE-488-Modus ist, kann das CBM-Bus-Kabel weiterhin angeschlossen bleiben, ohne andere CBM-Geräte zu stören
- Automatisches Kernal-Umschalten
- Alternatives Kernal möglich (in aktueller Firmware noch nicht aktiviert)
- LEDs zur Statusanzeige


# Firmware-Flashen

Zum Aufspielen der Firmware habe ich einen 6-poligen Header (auf der Rückseite der Platine) vorgesehen. Die Pins sind entsprechend beschriftet.

Am einfachsten geht dies mit dem Tool **xc3sprog** und einem **FTDI FT232H**-Adapter. Solche Adapter gibt es aus China für etwa 7 Dollar, in Deutschland kosten sie ca. 15 Euro.

Eine sehr gute Anleitung zur Verbindung und zum Flashen der JED-Datei mit xc3sprog findest du hier:
[https://github.com/1c3d1v3r/neatPLA/tree/master/programming](https://github.com/1c3d1v3r/neatPLA/tree/master/programming)

Die Pinbelegung ist wie folgt:

![](https://codeberg.org/diwou/TriMod_2.0_Adapter/raw/branch/main/Images/TriMod_Adapter_2.0_pin_header.jpg)

Die Pins für Kernal 2 bzw. einen zweiten Kernal sind derzeit nicht aktiv. Sie sind vorgesehen, falls in beiden Modi ein anderer Kernal benötigt wird, z. B. einmal SpeedDOS und einmal Original.

Die untere Stiftleiste ist zweireihig, die rechte Seite ist immer GND. Somit können ggf. Jumper gesteckt werden, um den Modus oder die Geräte-ID zu ändern.

Achtung: Sobald die Geräte-ID oder der Modus geändert wird, wird die 1541 automatisch zurückgesetzt. Das sollte nicht während eines Schreibvorgangs passieren!

Kernal 1 ist einfach mit einem 2564-Kernal-Adapter verbunden. Das Signal ist LOW im CBM-Bus-Modus und HIGH im GPIB- (IEEE-488-) Modus.

Um den IEC-Modus zu aktivieren, einfach den "Mode"-Pin mit GND verbinden oder einen Jumper setzen. Um den IEEE-488-Modus zu aktivieren, den Jumper wieder entfernen.

Die Geräte-ID wird wie üblich geschaltet: Für Gerät 8 müssen beide Jumper geschlossen bzw. beide Pins mit GND verbunden sein.

Geplant ist auch die Abfrage der Lötjumper auf der 1541. Diese Funktion ist aktuell noch nicht aktiviert, kann aber in der Firmware nachgerüstet werden.


## Stückliste (BOM)

Hier ist die Liste der benötigten Bauteile:

| Menge | Bezeichnung         | Hersteller         | Herstellernummer              | Beschreibung |
|-------|---------------------|--------------------|-------------------------------|--------------|
| 10    | C1–C12 (außer C3/C4) | KEMET              | C0603C104J3RACTU              | KerKo 0.1µF, 25V, X7R, 0603 |
| 2     | C3, C4              | KEMET              | C0805C106K8RACTU              | KerKo 10µF, 10V, X7R, 0805 |
| 2     | CN1, CN2           | Preci-Dip          | 830-10-020-10-001101          | 20-pol. 2mm Stiftleiste |
| 1     | CN3                | MPE-Garry          | 369-1-010-0-NTX-KT0           | MicroMatch-Buchse, 10-pol. |
| 1     | CN4                | MPE-Garry          | 369-1-024-0-NTX-KT0           | MicroMatch-Buchse, 24-pol. |
| 1     | CN5                | Sullins            | PRPC003SFAN-RC                | 3-pol. Stiftleiste |
| 1     | CN6                | Sullins            | PRPC006SFAN-RC                | 6-pol. vertikale Stiftleiste |
| 1     | CN7                | Sullins            | PRPC005SFAN-RC                | 5-pol. vertikale Stiftleiste |
| 1     | D1, D2             | Wurth              | 150060BS55040                 | Blaue LED, 0603 |
| 1     | D3                 | Wurth              | 150060SS55040                 | Rote LED, 0603 |
| 1     | D4                 | Wurth              | 150060YS55040                 | Gelbe LED, 0603 |
| 2     | Q1, Q2             | Infineon           | BCR135                        | NPN-Digitaltransistor, SOT-23 |
| 4     | R1–R4              | Yageo              | RC0603FR-071KL                | 1kΩ Widerstand, 0603 |
| 1     | RN1                | Yageo              | TC124-FR-0710KL               | Widerstandsarray 4x10kΩ, 0804 |
| 1     | U1                 | Exar               | SPX5205M5-L-3-3/TR            | LDO 3.3V Regler, SOT-23 |
| 1     | U2                 | Texas Instruments  | SN75160BDWR                   | GPIB-Treiber |
| 1     | U3                 | Texas Instruments  | SN75161BDWR                   | GPIB-Treiber |
| 1     | U4                 | Xilinx             | XC95144XL-10TQ100C            | CPLD, 144 Macrocell, 100 TQFP |



## Lizenz

Der Inhalt dieses Repositories (mit Ausnahme der Verzeichnisse "Docs" und "Software") unterliegt folgender Lizenz:

- [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0)](https://creativecommons.org/licenses/by-nc-sa/4.0/)

<<<<<<< HEAD


## License

The contents of this repository, with the exception of the Docs and Software directories, are released under the following license:

- the "Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License" (CC BY-NC-SA 4.0) full text of this license is included in the [LICENSE.CC-NC-BY-SA-4.0](https://codeberg.org/diwou/TriMod_2.0_Adapter/raw/branch/main/LICENSE.CC-NC-BY-SA) file and a copy can also be found at https://creativecommons.org/licenses/by-nc-sa/4.0/
=======
Der vollständige Lizenztext ist in der Datei [LICENSE.CC-NC-BY-SA-4.0](https://codeberg.org/diwou/TriMod_2.0_Adapter/raw/branch/main/LICENSE.CC-NC-BY-SA) enthalten.
>>>>>>> b324f39 (Text geändert)

