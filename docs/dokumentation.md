# Helmet Through Time – Web AR Prototyp
## Dokumentation HCI Aufgabe 1.1

---

## 1. Projektziel

Ziel dieses Projekts war die Entwicklung eines interaktiven Web-AR-Prototyps auf Basis bestehender Figma-Prototypen. Die Webapp ermöglicht es Nutzern, historische und moderne Feuerwehr-Objekte in Augmented Reality zu betrachten. Der Prototyp umfasst mindestens drei Seiten und mindestens drei 3D-Modelle, die direkt im Raum des Nutzers platziert werden können.

---

## 2. Plattformentscheidung: iOS

Der Prototyp wurde ausschliesslich für **iOS** entwickelt. Die gesamte Gruppe nutzt iPhones; Android-Geräte waren nicht verfügbar. Entsprechend wurde **AR Quick Look** (Apples nativer AR-Viewer in Safari) als AR-Technologie gewählt. Für Android wäre alternativ Scene Viewer (Google) über GLB-Dateien möglich gewesen.

AR Quick Look hat folgende Voraussetzungen:
- Browser: Safari auf iOS
- Dateiformat: **USDZ** (Universal Scene Description, gezippt)
- HTML-Einbindung: `<a rel="ar" href="model.usdz"><img …></a>`

---

## 3. Getestetes Gerät

| Eigenschaft | Wert |
|---|---|
| Gerät | iPhone 16 |
| Betriebssystem | iOS 26.4.2 |
| Browser | Safari |

---

## 4. Verwendete Technologien

| Technologie | Zweck |
|---|---|
| HTML / CSS / JavaScript | Webapp (kein Framework) |
| USDZ | 3D-Modellformat für iOS AR Quick Look |
| GLB / glTF | 3D-Modellformat (Referenz, nicht für AR genutzt) |
| Blender 5.1.1 | 3D-Modellierung und Export |
| GitHub Pages | Öffentliches Hosting der Webapp |
| Safari (iOS) | AR Quick Look Viewer |

---

## 5. Projektstruktur

```
/
├── index.html          Startseite mit Projektbeschreibung
├── collection.html     Übersicht aller Objekte
├── detail.html         Detailansicht mit AR-Button
├── style.css           Gemeinsames Styling (mobile-first, Dark Mode)
├── app-data.js         Datendatei mit allen Objekten
├── assets/
│   ├── historic_helmet.svg
│   ├── red_helmet.svg
│   ├── extinguisher.svg
│   └── axe.svg
├── models/
│   ├── fire_axe.usdz
│   ├── fire_axe.glb
│   ├── historic_helmet.usdz
│   ├── historic_helmet.glb
│   ├── red_helmet.usdz
│   ├── red_helmet.glb
│   ├── fire_extinguisher.usdz
│   └── fire_extinguisher.glb
└── docs/
    └── dokumentation.md
```

---

## 6. Beschreibung der Webapp

Die Webapp „Helmet Through Time" ist ein mobile-first Web-AR-Prototyp, der Feuerwehr-Objekte interaktiv erlebbar macht. Der Nutzer navigiert von einer Startseite über eine Objektübersicht zu einer Detailansicht, von der aus ein 3D-Modell direkt in AR geöffnet werden kann.

Das Design ist auf iPhone optimiert: dunkles Farbschema, grosse Touch-Targets, einfache Navigation ohne Menü-Komplexität.

---

## 7. Seiten

### Seite 1: Startseite (`index.html`)

Die Startseite stellt das Projekt vor und gibt dem Nutzer einen ersten Überblick. Ein zentraler Button führt zur Objektsammlung.

### Seite 2: Sammlung (`collection.html`)

Listenansicht aller vier Objekte als Karten mit Thumbnail, Name und kurzem Hinweis. Jede Karte führt zur Detailansicht des jeweiligen Objekts.

### Seite 3: Detailansicht (`detail.html`)

Zeigt ein einzelnes Objekt mit Vorschaubild, Titel, Beschreibung und dem zentralen „In AR ansehen"-Button. Über Pfeile kann zwischen Objekten navigiert werden.

---

## 8. 3D-Modelle

### Modell 1: Feuerwehraxt (`fire_axe.usdz`)

Selbst modelliert in Blender 5.1.1. Besteht aus zwei Mesh-Objekten: Axtkopf (Cube) und Stiel (Cylinder), mit unterschiedlichen Materialien (Metall, Holz). Exportiert direkt aus Blender als USDZ.

**Dateigrösse:** GLB 45 KB, USDZ 85 KB

### Modell 2: Historischer Lederhelm (`historic_helmet.usdz`)

Feuerwehrhelm aus der Zeit um 1900. Bestand aus gehärtetem Leder. Low-poly Modell.

**Dateigrösse:** GLB 32 KB, USDZ 56 KB

### Modell 3: Moderner Einsatzhelm (`red_helmet.usdz`)

Zeitgenössischer Feuerwehrhelm aus Kunststoff/Kevlar mit Visier und Nackenschutz.

**Dateigrösse:** GLB 187 KB, USDZ 348 KB

### Modell 4: Feuerlöscher (`fire_extinguisher.usdz`)

Standardfeuerlöscher. Ermöglicht Grössenvergleich im eigenen Raum durch AR.

**Dateigrösse:** GLB 609 KB, USDZ 879 KB

---

## 9. Workflow: Feuerwehraxt (vollständig dokumentiert)

Der vollständige Workflow wird exemplarisch anhand der Feuerwehraxt dokumentiert, da dieses Modell selbst erstellt wurde. Die übrigen Modelle lagen bereits als USDZ vor.

### Schritt 1: Ausgangspunkt in Blender

Das Modell wurde in Blender 5.1.1 erstellt. Es besteht aus zwei Objekten:
- **Cube**: Axtkopf, Material: Metall (grau)
- **Cylinder**: Stiel, Material: Holz (beige)

*→ Screenshot A: Blender Viewport (Solid Mode) mit Feuerwehraxt*
*→ Screenshot B: Blender Viewport (Material Preview) mit sichtbaren Materialfarben*

Die Szene zeigte beim Öffnen eine Warnung: **„Active object has non-uniform scale"** (Scale Y: 1.240). Dies bedeutet, dass die Skalierung nicht auf die Geometrie angewendet wurde, was beim Export zu falschen Proportionen führen kann.

### Schritt 2: Vorbereitung – Transforms anwenden

Vor dem Export wurde die Skalierung korrigiert:

1. Alle Objekte selektieren: `A`
2. Apply-Menü öffnen: `Ctrl + A`
3. **„All Transforms"** wählen

*→ Screenshot C: Apply-Menü in Blender mit „All Transforms" markiert*

Nach diesem Schritt war die Warnung nicht mehr sichtbar.

### Schritt 3: Export als USDZ

Export-Pfad in Blender: **File → Export → Universal Scene Description (.usd\*)**

*→ Screenshot D: Blender Menü mit geöffnetem Export-Untermenü*

**Problem beim Export:** Beim ersten Exportversuch wurde versehentlich die Dateiendung `.usdc` statt `.usdz` gewählt. `.usdc` ist ein binäres USD-Format, das von iOS Safari und AR Quick Look **nicht** als AR-Datei erkannt wird. Der Fehler wurde bemerkt und korrigiert.

**Lösung:** Dateiname im Export-Dialog manuell auf `3d_object_fireaxe_export.usdz` geändert und erneut exportiert.

*→ Screenshot E: Export-Dialog mit falschem Dateinamen (.usdc) – erster Versuch*
*→ Screenshot E2: Export-Dialog mit korrigiertem Dateinamen (.usdz)*

**Verwendete Export-Einstellungen:**
- Format: USDZ
- Include: Meshes ✅
- Animation: nicht aktiviert
- Units: Meters

### Schritt 4: Einbindung in HTML mit AR Quick Look

[→ wird nach Website-Bau ergänzt]

### Schritt 5: Test auf iPhone 16

[→ wird nach Deployment ergänzt]

---

## 10. AR Quick Look Einbindung

AR Quick Look ist Apples nativer AR-Viewer, der direkt in iOS Safari integriert ist. Er öffnet sich automatisch wenn ein Link mit `rel="ar"` angetippt wird und die verlinkte Datei eine `.usdz`-Datei ist.

**Technische Anforderung:** Apple verlangt, dass das `<a rel="ar">`-Element ein `<img>`-Element als direktes Kind enthält. Ohne dieses `<img>` erkennt iOS Safari den Link nicht als AR-Trigger und öffnet die Datei stattdessen als Download oder zeigt sie im normalen Browser an.

**Implementierung in `detail.html` (Zeilen 42–46):**

```html
<a class="btn ar-btn" id="arBtn" rel="ar" href="models/fire_axe.usdz">
  <img id="arImg" src="assets/axe.svg" alt=""
       style="position:absolute;width:0;height:0;overflow:hidden">
  In AR ansehen
</a>
```

Das `<img>`-Element wird auf 0×0 Pixel gesetzt (`width:0;height:0`), damit es unsichtbar ist und der Button wie ein normaler Button aussieht. `position:absolute` und `overflow:hidden` verhindern, dass es Layout-Platz einnimmt. Das `href`-Attribut des `<a>`-Elements zeigt auf die USDZ-Datei.

*→ Screenshot F: VS Code mit AR Quick Look HTML-Code, Kommentar und Button-Implementierung sichtbar*

**Warum nicht einfach `display:none`?** Mit `display:none` wird das Element komplett aus dem DOM-Rendering entfernt. Manche iOS-Versionen prüfen ob das `<img>`-Kind gerendert wird, bevor AR Quick Look aktiviert wird. `width:0;height:0` ist die zuverlässigere Methode.

**Datenpflege über JavaScript:** Die `href`- und `src`-Attribute werden dynamisch gesetzt, damit dieselbe `detail.html`-Seite für alle vier Objekte funktioniert:

```javascript
arBtn.href = item.usdz;   // z.B. "models/fire_axe.usdz"
arImg.src  = item.image;  // z.B. "assets/axe.svg"
```

---

## 11. GitHub Pages Deployment

[→ wird nach Deployment ergänzt]

---

## 12. Probleme und Lösungen

| Problem | Ursache | Lösung |
|---|---|---|
| Export als `.usdc` statt `.usdz` | Dateiendung im Export-Dialog nicht manuell gesetzt | Dateiname im Dialog auf `.usdz` geändert und erneut exportiert |
| Non-uniform scale Warnung | Scale wurde nicht auf Geometrie angewendet | `Ctrl+A → All Transforms` vor Export |
| AR-Button funktioniert nicht auf iOS | `<a rel="ar">` ohne `<img>`-Kind-Element | AR Quick Look Pattern korrekt implementiert (siehe Abschnitt 10) |
| Falsche Dateistruktur für GitHub Pages | Dateien in verschachteltem Unterordner | Alle Dateien in Repo-Root verschoben |

---

## 13. Reflexion / Limitations

[→ wird am Ende ergänzt]

---

## 14. Fazit

[→ wird am Ende ergänzt]

---

*Screenshots werden als separate Bilddateien in `docs/screenshots/` abgelegt und sind in diesem Dokument referenziert.*
