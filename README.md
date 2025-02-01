Verwendete Palette: 


# Anleitung: Zigbee-Schalter mit Loxone verbinden

## 1. Voraussetzungen
- Ein funktionierender **Zigbee2MQTT-Server**
- Ein **Zigbee-Schalter**, der von Zigbee2MQTT unterstützt wird
- Ein laufender **Loxone Miniserver**
- **Node-RED** installiert und eingerichtet
- **Zigbee2MQTT** installiert und eingerichtet
- Zugriff auf das Node-RED-Interface
- node-red-contrib-zigbee2mqtt 2.7.4 intsalliert

## 2. Funktionsweise des Node-RED-Flows
Der bereitgestellte Flow erlaubt die Integration eines Zigbee-Schalters mit einem virtuellen Eingang in Loxone. 
Der Flow besteht aus mehreren Elementen:

1. **Zigbee2MQTT-Input (TestSchalter)**: Empfängt Schalteraktionen über MQTT.
2. **Switch-Node**: Analysiert die empfangenen Aktionen und leitet sie an die entsprechenden Ausgänge weiter.
3. **Change-Nodes**: Wandeln die Aktionen in Zahlenwerte für die Loxone-Schnittstelle um.
4. **HTTP-Request-Node**: Sendet den Befehl an Loxone.
5. **Comment-Node**: Enthält hilfreiche Informationen zur Loxone-Konfiguration.

## 3. Installation und Konfiguration
### 3.1. Import des Flows in Node-RED
1. Öffne **Node-RED**.
2. Klicke auf das Menü (oben rechts) und wähle **Import > Clipboard**.
3. Kopiere den bereitgestellten JSON-Flow und füge ihn in das Textfeld ein.
4. Klicke auf **Importieren**.
5. Platziere den Flow im Arbeitsbereich und speichere die Änderungen.

### 3.2. Konfiguration des Zigbee2MQTT-Servers
1. Stelle sicher, dass Zigbee2MQTT korrekt installiert und gestartet ist.
2. Der **Base-Topic** in Zigbee2MQTT sollte auf `zigbee2mqtt` gesetzt sein.
3. Der **Zigbee-Schalter** muss in Zigbee2MQTT erkannt werden (siehe `friendly_name`).

### 3.3. Anpassung der Loxone-URL
1. Öffne den **Build URL Node**.
2. Ersetze `<MINISERVER IP>` durch die IP-Adresse deines Loxone Miniservers.
3. Ersetze `<NAME VOM VIRTUELLEN EINGANG>` mit dem Namen des entsprechenden virtuellen Eingangs.
4. Speichere die Änderungen.

### 3.4. Testen des Flows
1. Starte den Flow in Node-RED.
2. Betätige den Zigbee-Schalter und überprüfe, ob die entsprechenden Nachrichten in Node-RED ankommen.
3. Kontrolliere in Loxone, ob die virtuellen Eingänge entsprechend geschaltet werden.

## 4. Werteübersicht für den Binär-Decodierer
Loxone benötigt zur Verarbeitung der Schalterzustände einen Binär-Decodierer:

| Gesendeter Wert | Ausgang (Q) |
|----------------|------------|
| 1 | Q1 |
| 2 | Q2 |
| 4 | Q3 |
| 8 | Q4 |

## 5. Fehlerbehebung
- **Zigbee-Schalter wird nicht erkannt**: Prüfe, ob Zigbee2MQTT korrekt läuft und der Schalter gepairt ist.
- **Keine Reaktion in Loxone**: Überprüfe die **Miniserver-IP** und den Namen des virtuellen Eingangs.
- **Node-RED zeigt keine Daten an**: Kontrolliere den MQTT-Server und ob die Nachrichten korrekt empfangen werden.

## 6. Fazit
Mit diesem Node-RED-Flow kann ein Zigbee-Schalter einfach in ein Loxone Smart Home integriert werden. Durch die flexible Anpassung lassen sich auch weitere Schalter oder Funktionen hinzufügen.
