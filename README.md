## Athena Crop Steering Blueprint – Anleitung

---

### 🌱 **Überblick**

Dieses Blueprint automatisiert die Bewässerung und das Crop Steering für den professionellen Cannabisanbau nach der **Athena Precision Irrigation Strategy**. Es unterstützt verschiedene Substrate und Topfgrößen, steuert EC, Runoff, Trockenphasen (Dryback) und bietet Notfallfunktionen.

---

### 🪴 **Unterstützte Substrate & Topfgrößen**

- **4" Rockwool (Delta 6.5)**
- **1 Gallon Coco (3,7L)**
- **8L Coco Professional**
- **11L Coco XXL**
- **Hugo 6" Slab**

---

### ⚙️ **Funktionen im Überblick**

#### 1. **Substrat- und Phasenauswahl**
- Wähle im Blueprint dein Substrat und die aktuelle Wachstumsphase:
  - **Veg**
  - **Stretch**
  - **Flower Bulk**
  - **Flower Finish**

#### 2. **Automatische Shot- und Runoff-Berechnung**
- Für jede Topfgröße werden die optimalen Shot-Volumina und Runoff-Zielwerte aus der Athena-Strategie verwendet.

#### 3. **P1-Phase (Sättigung)**
- Startet ca. 90 Minuten nach Licht an.
- Führt mehrere kleine Bewässerungsimpulse (Shots) aus, bis das Runoff-Ziel erreicht ist.
- Verhindert Channeling und Überwässerung.

#### 4. **P2/P3-Phasen (Erhaltung & Dryback)**
- Überwacht die Substratfeuchte (VWC).
- Startet Bewässerung, wenn das gewünschte Dryback (prozentualer Feuchteverlust) erreicht ist.
- Unterschiedliche Zielwerte für vegetative und generative Phasen.

#### 5. **EC-Management**
- Überwacht den Substrat-EC.
- Bei Überschreitung des Maximums wird automatisch eine Spülung ausgelöst und eine Benachrichtigung gesendet.

#### 6. **Notfall- und Sicherheitsfunktionen**
- Alarm bei zu geringem Runoff nach P1.
- Alarm und Spülung bei zu hohem EC.
- Alle Benachrichtigungen werden an dein gewähltes Gerät gesendet.

#### 7. **Dashboard-Integration**
- Empfohlen: Erstelle ein Lovelace-Dashboard mit EC-, VWC- und Runoff-Anzeigen sowie manuellem Override.

---

### 🛠️ **Installation & Anwendung**

1. **Dateien kopieren**
   - Speichere die YAML-Datei als `athena_crop_steering_blueprint.yaml` im Verzeichnis `/config/blueprints/automation/` deines Home Assistant.
   - Lege die README.txt im gleichen Ordner oder im Hauptverzeichnis deines Projekts ab.

2. **Blueprint importieren**
   - Gehe in Home Assistant zu **"Automatisierungen & Szenen" → "Blueprints" → "Importieren"**.
   - Wähle die YAML-Datei aus.

3. **Automatisierung erstellen**
   - Erstelle eine neue Automatisierung auf Basis des Blueprints.
   - Wähle Substrat, Wachstumsphase, Sensoren und Geräte entsprechend deiner Hardware aus.

4. **Sensoren korrekt platzieren**
   - **Feuchtesensor:** 5–10 cm unter Substratoberfläche (je nach Topfgröße)
   - **EC-Sensor:** Im Abflussbereich
   - **Runoff-Sensor:** Am Ablauf installieren

5. **Testlauf & Feintuning**
   - Überwache die ersten Zyklen und passe ggf. Shot-Volumen oder Sensorposition an.
   - Kontrolliere Runoff und EC regelmäßig manuell zur Kalibrierung.

---

### 📊 **Parameter-Tabellen**

| Topfgröße         | 1% Shot | Veg Runoff (8–16%) | Gen Runoff (1–7%) | Veg Dryback (%) | Gen Dryback (%) | EC-Range (mS/cm) |
|-------------------|---------|--------------------|-------------------|-----------------|-----------------|------------------|
| 3,7L Coco         | 37 ml   | 296–592 ml         | 37–259 ml         | 25–35           | 40–50           | 3.2–10.5         |
| 8L Coco           | 80 ml   | 640–1280 ml        | 80–560 ml         | 30–40           | 45–55           | 3.5–11.2         |
| 11L Coco          | 110 ml  | 880–1760 ml        | 110–770 ml        | 35–45           | 50–60           | 3.8–12.0         |
| Hugo 6" Slab      | 100 ml  | 280–560 ml         | 35–245 ml         | 30–40           | 40–50           | 3–6              |
| 4" Rockwool       | 6.5 ml  | 56–112 ml          | 7–46 ml           | 30–40           | 40–50           | 3–6              |

---

### 💡 **Hinweise & Tipps**

- **Dryback:** Je größer das Dryback, desto stärker der generative Steuerimpuls (kompaktere Pflanzen, mehr Blütenansatz).
- **EC:** Zu hohe EC-Werte vermeiden, da sonst Salzstress und Wachstumsstörungen drohen.
- **Runoff:** Kontrolliere regelmäßig, ob die Zielwerte erreicht werden – dies ist entscheidend für die Steuerung des Substrat-EC.
- **Sensor-Kalibrierung:** Sensoren regelmäßig kalibrieren und auf Plausibilität prüfen.
- **Fehlermeldungen:** Werden als Push-Nachricht oder E-Mail (je nach Einstellung) ausgegeben.

---

### 🔄 **Erweiterungen & Anpassungen**

- **Multi-Zonen-Bewässerung:** Möglich durch Kopieren und Anpassen der Automatisierung.
- **Integration weiterer Sensoren:** (z.B. Temperatur, Luftfeuchte, CO₂) für fortgeschrittenes Crop Steering möglich.
- **Individuelle Anpassung:** Shot- und Runoff-Werte können an Sorten oder Bedingungen angepasst werden.

### 🛠️ **Beispiel Node-RED-Flow**

Im Ordner `node_red/` befindet sich die Datei `simple_irrigation_flow.json`. Sie
enthält einen einfachen Bewässerungsablauf, der einen Feuchtigkeitssensor
auswertet und bei Bedarf eine Wasserpumpe einschaltet. Der Flow kann in
Node-RED über das Import-Menü geladen und an die eigenen Hardware-Gegebenheiten
angepasst werden.

---

### 📚 **Support & Quellen**

- Siehe Originaldokumentation von Athena Ag oder nutze die Home Assistant Community.
- Die Strategie basiert auf der offiziellen [Precision Irrigation Strategy von Athena Ag](https://athenaag.com/irrigation-strategy).

---


