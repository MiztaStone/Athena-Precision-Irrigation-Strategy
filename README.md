# Athena Precision Irrigation Blueprint

![Crop Steering](https://via.placeholder.com/800x400)

## 📋 Funktionsübersicht
- **3-Phasen Automatisierung** (P1 Sättigung, P2 Erhaltung, P3 Trockenphase)
- **EC-Management** mit adaptiven Schwellenwerten
- **Multi-Substrat-Unterstützung** (Coco 3.7L/8L/11L, Steinwolle)
- **Sicherheitssysteme** (EC-Notfallspülung, Leckageerkennung)

## 🛠 Installation
1. Blueprint-Datei in `/config/blueprints/automation/` speichern
2. In Home Assistant: *Einstellungen > Automatisierungen > Blueprint importieren*
3. GitHub-URL eingeben: `https://github.com/[DEIN-USER]/crop-steering/blob/main/crop_steering_athena.yaml`

## ⚙️ Konfiguration
| Parameter          | Beschreibung                      |
|--------------------|-----------------------------------|
| `substrate_type`   | Volumen & Drainageverhalten       |
| `growth_phase`     | Veg/Blüte-EC-Zielwerte            |
| `ec_max`           | Abschaltgrenze bei Überdüngung    |

**Beispiel-Sensorik:**

sensor:

platform: moisture
name: "Substratfeuchte"

platform: conductivity
name: "EC-Wert"



## 🔄 Automatisierungslogik
### P1-Sättigungsphase
- Startet 90min nach Lichteinschaltung
- 2-6% Schüsse im 15-Minuten-Takt
- Abbruch bei 5-15% Runoff

**Formel:**  
\( \text{Bewässerungszeit} = \frac{\text{Substratvolumen} \times 0.02}{\text{Durchflussrate}} \)


### EC-Stacking Algorithmus

if current_ec < target_ec:
reduce_shot_size()
elif current_ec > target_ec:
increase_runoff()


## 🚨 Sicherheitsfeatures
1. **Automatische Spülung** bei EC > 12 mS/cm
2. **Dreifache Sensorredundanz** für Feuchtemessung
3. **Leckageerkennung** durch Durchflussmesser

## 📈 Best Practices
- **Sensorplatzierung:** 5cm unter Substratoberfläche
- **Kalibrierung:** Wöchentliche EC-Kontrolle per Handmessgerät
- **Notfallprozedur:** Manueller Dryback-Override bei Wurzelfäule

## 📚 Ressourcen
- [Athena Irrigation Strategy PDF](https://athenaag.com/irrigation-strategy)
- [Home Assistant Blueprint Docs](https://www.home-assistant.io/docs/blueprint)





Athena Crop Steering Blueprint V2– Anleitung
Überblick
Dieses Blueprint automatisiert die Bewässerung und das Crop Steering für den professionellen Cannabisanbau nach der Athena Precision Irrigation Strategy. Es unterstützt verschiedene Substrate und Topfgrößen, steuert EC, Runoff, Trockenphasen (Dryback) und bietet Notfallfunktionen.

Unterstützte Substrate/Topfgrößen
4" Rockwool (Delta 6.5)

1 Gallon Coco (3,7L)

8L Coco Professional

11L Coco XXL

Hugo 6" Slab

Funktionen im Überblick
1. Substrat- und Phasenauswahl

Wähle im Blueprint dein Substrat und die aktuelle Wachstumsphase (Veg, Stretch, Flower Bulk, Flower Finish).

2. Automatische Shot- und Runoff-Berechnung

Das System verwendet für jede Topfgröße die optimalen Shot-Volumina und Runoff-Zielwerte aus der Athena-Strategie.

3. P1-Phase (Sättigung)

Startet ca. 90 Minuten nach Licht an.

Führt mehrere kleine Bewässerungsimpulse (Shots) aus, bis das Runoff-Ziel erreicht ist.

Verhindert Channeling und Überwässerung.

4. P2/P3-Phasen (Erhaltung & Dryback)

Überwacht die Substratfeuchte (VWC).

Startet Bewässerung, wenn das gewünschte Dryback (prozentualer Feuchteverlust) erreicht ist.

Unterschiedliche Zielwerte für vegetative und generative Phasen.

5. EC-Management

Überwacht den Substrat-EC.

Bei Überschreitung des Maximums wird automatisch eine Spülung ausgelöst und eine Benachrichtigung gesendet.

6. Notfall- und Sicherheitsfunktionen

Alarm bei zu geringem Runoff nach P1.

Alarm und Spülung bei zu hohem EC.

Alle Benachrichtigungen werden an dein gewähltes Gerät gesendet.

7. Dashboard-Integration

Empfohlen: Erstelle ein Lovelace-Dashboard mit EC-, VWC- und Runoff-Anzeigen sowie manuellem Override.

Installation & Anwendung
Dateien kopieren

Speichere die YAML-Datei als athena_crop_steering_blueprint.yaml im Verzeichnis /config/blueprints/automation/ deines Home Assistant.

Lege die README.txt im gleichen Ordner oder im Hauptverzeichnis deines Projekts ab.

Blueprint importieren

Gehe in Home Assistant zu "Automatisierungen & Szenen" → "Blueprints" → "Importieren".

Wähle die YAML-Datei aus.

Automatisierung erstellen

Erstelle eine neue Automatisierung auf Basis des Blueprints.

Wähle Substrat, Wachstumsphase, Sensoren und Geräte entsprechend deiner Hardware aus.

Sensoren korrekt platzieren

Feuchtesensor: 5–10 cm unter Substratoberfläche (je nach Topfgröße)

EC-Sensor: Im Abflussbereich

Runoff-Sensor: Am Ablauf installieren

Testlauf & Feintuning

Überwache die ersten Zyklen und passe ggf. Shot-Volumen oder Sensorposition an.

Kontrolliere Runoff und EC regelmäßig manuell zur Kalibrierung.

Parameter-Tabellen (Auszug)
Topfgröße	1% Shot	Veg Runoff (8–16%)	Gen Runoff (1–7%)	Veg Dryback (%)	Gen Dryback (%)	EC-Range (mS/cm)
3,7L Coco	37 ml	296–592 ml	37–259 ml	25–35	40–50	3.2–10.5
8L Coco	80 ml	640–1280 ml	80–560 ml	30–40	45–55	3.5–11.2
11L Coco	110 ml	880–1760 ml	110–770 ml	35–45	50–60	3.8–12.0
Hugo 6" Slab	100 ml	280–560 ml	35–245 ml	30–40	40–50	3–6
4" Rockwool	6.5 ml	56–112 ml	7–46 ml	30–40	40–50	3–6
Hinweise & Tipps
Dryback: Je größer das Dryback, desto stärker der generative Steuerimpuls (kompaktere Pflanzen, mehr Blütenansatz).

EC: Zu hohe EC-Werte vermeiden, da sonst Salzstress und Wachstumsstörungen drohen.

Runoff: Kontrolliere regelmäßig, ob die Zielwerte erreicht werden – dies ist entscheidend für die Steuerung des Substrat-EC.

Sensor-Kalibrierung: Sensoren regelmäßig kalibrieren und auf Plausibilität prüfen.

Fehlermeldungen: Werden als Push-Nachricht oder E-Mail (je nach Einstellung) ausgegeben.

Erweiterungen & Anpassungen
Multi-Zonen-Bewässerung möglich durch Kopieren und Anpassen der Automatisierung.

Integration von weiteren Sensoren (z.B. Temperatur, Luftfeuchte, CO2) für fortgeschrittenes Crop Steering möglich.

Anpassung der Shot- und Runoff-Werte an individuelle Sorten oder Bedingungen jederzeit möglich.

Für Rückfragen oder Support:

Siehe Originaldokumentation von Athena Ag oder nutze die Home Assistant Community.

Die Strategie basiert auf der offiziellen [Precision Irrigation Strategy von Athena Ag].: https://athenaag.com/irrigation-strategy
