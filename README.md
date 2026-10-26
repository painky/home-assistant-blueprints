# Home Assistant Blueprints

Sammlung eigener Automatisierungs-Blueprints für Home Assistant.

## Lichtsteuerung: Lux, Nachlauf und Bypass (V2)

Datei: [`automation/light/light_lux_bypass_timer.yaml`](automation/light/light_lux_bypass_timer.yaml)

### Funktionen

- Mehrere Eingänge: `switch`, `binary_sensor` oder `input_boolean`.
- Einschalten bei einer neuen `off → on`-Flanke, wenn der Helligkeitssensor einen gültigen Wert unter dem Lux-Grenzwert meldet.
- Ausschalten nach einstellbarer Nachlaufzeit (Standard: 2 Minuten), wenn alle Eingänge eindeutig `off` melden.
- `unknown` und `unavailable` lösen keine Flankenschaltung aus; ein gestörter Eingang verhindert automatisches Ausschalten.
- Eine neue `off → on`-Flanke eines Bypass-Schalters schaltet die Lampen um, unabhängig von der Helligkeit.
- Der Bypass wird nach einer konfigurierbaren Maximaldauer (Standard: 2 Stunden) zurückgesetzt, ohne die Lampen zu schalten.

### Installation

1. YAML-Datei nach `/config/blueprints/automation/custom/light_lux_bypass_timer.yaml` kopieren.
2. Home Assistant → **Einstellungen → Automatisierungen & Szenen → Blueprints** öffnen und Blueprints neu laden.
3. Über den Blueprint eine Automatisierung erstellen und Eingänge, Lux-Sensor, Lampen und Bypass auswählen.

### Wichtige Hinweise

- Der Bypass muss eine **steuerbare** `switch`- oder `input_boolean`-Entität sein. Die Automatisierung setzt diese Entität nach der Maximaldauer wieder auf `off`.
- Eine bereits aktive Eingangs-Entität schaltet die Lampe nach einem Bypass-Umschalten nicht automatisch wieder ein; dafür ist eine neue `off → on`-Flanke erforderlich.
- Die Nachlaufzeit ist als `for:` im Zustands-Trigger implementiert. Diese Zeitmessung übersteht keinen Neustart oder Reload der Automatisierungen.
- Die Nachlaufzeit startet pro `on → off`-Flanke. Sind mehrere Eingänge aktiv, kann ein späterer Wechsel des letzten Eingangs das Ausschalten verzögern.
- Der Blueprint ist nicht auf einer realen Home-Assistant-Installation getestet.

### Beispielwerte

| Einstellung | Wert |
| --- | --- |
| Helligkeitsgrenze | 100 lx |
| Nachlaufzeit | 2 Minuten |
| Maximale Bypass-Dauer | 2 Stunden |

## Lizenz

Noch keine Lizenz festgelegt.
