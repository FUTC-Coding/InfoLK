## TCP/IP

1. Anwendungsschicht
2. Transportschicht
3. Internetschicht
4. Netzzugangsschicht

## Anwendungsschicht

High-level Anwendungsprotokolle wie HTTP/HTTPS/SMTP/SSH usw.

## Transportschicht

Hier muss sicher gestellt werden, dass die Daten von einem Rechner zum anderen gesendet werden können

Bei paketbasierter Übertragung werden die Daten in Pakete aufgeteilt und separat durch das Netzwerk über unterschiedliche Routen geschickt und dann wieder beim Empfänger zusammengesetzt.

Die Aufteilung der Daten, die Segmentierung, erfolgt in der Transportschicht.

Der Sender einigt sich mit dem Empfänger auf eine Segmentgröße, in der Regel ca. 1500 Bytes.

Die Einigung gehört zur "Flow Control".

Jedes Segment hat einen TCP-Header.

Über die Acknowledgement number fordert der Empfänger jeweils das nächste Segment an.

In der Transportschicht wird auch die Verbindung zwischen den beiden beteiligten Systemen hergestellt.

Gemeinsam werden IP und Port benutzt um damit einen Socket zwischen einem Sender und einem Empfänger zu erstellen.

## Internetschicht

Die paketbasierte Übertragung ist technisch anspruchsvoller umzusetzen aber sichert im Zusammenhang mit einer (kompakten) teilmaschigen Topologie eine hohe Ausfallsicherheit des Netzwerkes.

Jedes Datenpaket muss mindestens fünf Informationen enthalten:

- Senderadresse, Zieladresse
- Länge des Datenteils
- Index des Pakets
- Priorität

### IPv4 Adressen

| 192      | 168      | 2        | 101      |
| -------- | -------- | -------- | -------- |
| 11000000 | 10101000 | 00000010 | 01100101 |
| 1Byte    | 1Byte    | 1Byte    | 1Byte    |

Insgesamt 4 Byte (32 bit)



Eine IP-Adresse besitzt Netzwerk- und Geräteteil, man bestimmt die beiden Teile über die Netzmaske

Besitzen Sender und Empfänger den gleichen Netzwerkteil, dann verbleiben die Pakete im lokalen Netz, ansonsten werden sie dem Internet übergeben.

Router entscheiden anhand Routingtabellen, die ständig aktualisiert werden, wo entlang das mit einer Zieladresse versehene Paket gesendet werden soll.

Jedes Paket bekommt von der Internetschicht den z.B. IPv4 header, für den Transport.

### Aktualisierung der Routingtabellen

Jeder Router besitzt eine Liste seiner Nachbarrouter mit den entsprechenden Kosten, um diesen zu erreichen

Diese Liste schickt er an alle seine Nachbarn die dann bisher noch nicht aufgeführte Router mit den entsprechenden Kosten aufnehmen und überprüfen ob es bessere Wege zu den schon bekannten Routern gibt.

### Berechnung von Netzwerk- und Geräteteil einer IP-Adresse in der Internetschicht

![Berechnung](https://github.com/Tanonic/InfoLK/blob/master/netzwerke/Scannable-Dokument%20am%2023.02.2019%2C%2016_18_44.png)

## Netzzugangsschicht

Der eigentliche physikalische Transport.

Die Bits werden z.B. als Stromimpulse oder Lichtwellen übertragen

### Mögliche Prüfverfahren

**Paritätsbit**	An die Bitfolge wird ein Prüfbit angehängt, durch das die Anzahl der Einsen in der Bitfolge gerade wird.

<u>Beispiel:</u> 10010111 | Berechnung: Anzahl Einsen ist ungerade | Prüfbit: 1

**Prüfsumme**	Es werden alle Bits der Bitfolge addiert. Die Summe wird modulo n gerechnet, wobei durch n die Länge der Prüfsumme bestimmt wird.

<u>Beispiel:</u> 10110111 | Berechnung: (1+0+1+1+0+1+1+1)mod4 | Prüfsumme: 10

**XOR-Prüfsumme** Mehrere gleich lange Teile einer Bitfolge werden XOR-verknüpft. Es entsteht eine Prüfsumme, die die gleiche Länge wie die einzelnen Bitfolgen hat.

<u>Beispiel:</u> 10110011 01101000 | Berechnung: XOR beide Bytes übereinander | Prüfsumme: 11011011

Beim Empfänger wird die Prüfsumme erneut ermittelt und mit der übertragenen verglichen - bei Unterschieden wir das Paket erneut angefordert.

Jeder Netzwerkadapter besitzt eine 48bit (6byte) lange Media-Access-Control (MAC-Adresse).

Jede Adresse sollte nur einmal vergeben werden.

In der Regel als hexadezimal notiert.

## Sicherheitsziele der Übertragung von Nachrichten in Netzwerken

**Vertraulichkeit**: Sicherstellung, dass die Nachricht nicht von unbefugten Dritten gelesen wurde.

**Integrität**: Sicherstellung, dass die Nachricht nicht durch unbefugte Dritte verändert wurde.

**Authentizität**: Sicherstellung, dass die Nachricht wirklich vom angegebenen Absender stammt (Nachrichtenauthentizität). Identifikation des Kommunikationspartners (Teilnehmerauthentizität).

**Nichtabstreitbarkeit**: Sicherstellung, dass der Absender der Nachricht nicht in der Lage ist, seine Urheberschaft zu bestreiten, d.h. soll sie gegenüber Dritten nachweisbar sein.

## Modulo

3 mod 7 = 3 (7 passt 0 mal in die 3, Rest 3)

### Regeln

1. (x+y) mod m = ((x mod m) + (y mod m)) mod m
2. (x * y) mod m = ((x mod m)*(y mod m)) mod m
3. x^y+z mod m = ((x^y mod m)*(x^z mod m)) mod m
4. x^y mod m = (x mod m)^y mod m

## Primfaktorzerlegung

100 = 10 * 10 = 2 * 5 * 2 * 5 = 2 * 2 * 5 * 5 = 2^2 * 5^2

130 = 2 * 65 = 2 * 5 * 13