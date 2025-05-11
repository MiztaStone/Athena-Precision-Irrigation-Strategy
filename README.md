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
