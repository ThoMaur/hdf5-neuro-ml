# HDF5 Neuro-ML – Spezifikation (`hdf5-neuro-ml`) – nur EEG

Dieses Dokument beschreibt den Standard für **HDF5-Dateien mit EEG-Daten**: Rohwellenformen, wie sie in der Datei abgelegt werden, und den **Bezug zu Rohdaten vs. verarbeiteten Daten**. Andere Modalitäten sind **nicht** Gegenstand dieser Spezifikation.

| Feld | Wert |
|------|------|
| **Format-Kennung** | `hdf5-neuro-ml` (HDF5-Attribut `format` an der Dateiwurzel) |
| **Aktuelle Version** | `1.2` (Attribut `format_version`) |
| **Referenz-Implementierung** | Conox (`conox_save.py`); BIS Advanced dieselbe Struktur, gerätespezifische Typen/Einheiten (`medtronic_bis_save.py`) |

---

## 1. Rohdaten vs. verarbeitete EEG-Daten (Begriffe)

In einer **Fenster-HDF5-Datei** (typisch z. B. 10 s) steckt **eine** zeitlich zusammenhängende EEG-Wellenform pro Kanal. Was „Roh“ und was „verarbeitet“ heißt, hängt von **Gerät** und **Pipeline** ab. Die Spezifikation macht das über das Root-Attribut **`processing_levels`** und die **Dataset-Attribute** (`unit`, …) nachvollziehbar.

### 1.1 Rohdaten (EEG)

**Rohdaten** im Sinne dieser Spezifikation sind die **sampleweise gespeicherte Wellenform**, so wie sie für Archivierung und Auswertung in der Datei landet — **ohne** zusätzliche ML- oder Klinik-Features (Indizes, Trendskalare), die **nicht** als Zeitreihe gleicher Länge wie `timestamps` mitabgelegt werden.

- **BIS Advanced:** Die Kanäle sind **`int16`-Zähler** (`unit`: `counts`) direkt aus dem Screen-EEG-Datenstrom. Root-Attribut **`processing_levels`**: typischerweise `["raw"]` — keine weitere Gerätekennzeichnung in dieser Datei.
- **Conox:** Die Kanäle sind **`float32` in µV** (`unit`: `µV`). Auf dem Gerät bzw. in der Pipeline laufen vorher Schritte (z. B. Entzerrung, Skalierung). Das wird semantisch über **`processing_levels`** dokumentiert, z. B. `["raw", "device_internal"]`: Die gespeicherte Kurve ist die **für das Archiv gewählte** Wellenform nach geräteinterner Verarbeitung, nicht die unbearbeitete Bitfolge aus dem Rohpaket.

Kurz: **„Roh“ in der HDF5-Datei** = die **EEG-Zeitreihe(n)** unter `signals/` mit der gemeinsamen Zeitachse — nicht die verarbeiteten **Skalarwerte** (qCON, BIS, …), die die Pipeline meist in **PostgreSQL** speichert.

### 1.2 Verarbeitete / abgeleitete EEG-Daten

**Verarbeitete** oder **abgeleitete** EEG-Inhalte sind alles, was **aus** der Wellenform gewonnen wird oder **zusätzliche** Verarbeitungsstufen darstellt, z. B.:

- **Außerhalb dieser HDF5-Fensterdatei:** Trendgrößen, Indizes, Monitoring-Tabellen → in der Regel **Datenbank**, nicht in der `.h5` pro 10-s-Fenster.
- **Innerhalb HDF5 (optional, zukünftig):** z. B. bandpass-gefilterte Kopie, Spektralmerkmale pro Fenster, eigene Datasets unter einem Zweig **`derived`**.

Wenn abgeleitete EEG-Datasets ergänzt werden, gehören sie **nicht** unter `raw/`, sondern unter **`derived/…`**, und ihre **Zeitbasis** und **Herkunft** müssen in Attributen oder unter `meta/` beschrieben sein.

---

## 2. Ziele und Geltungsbereich

- **Einheitliche Lesbarkeit** von EEG-Fenstern für Auswertung und ML.
- **Klare Trennung** zwischen gespeicherter Wellenform (**raw** im Sinne von Abschnitt 1) und optionalen **abgeleiteten** EEG-Datasets (**derived**).
- **Kompatibilität** mit der Pipeline unter `D:/eeg/...` (typisch **10 s** pro Datei).

---

## 3. Konventionen

| Konvention | Bedeutung |
|------------|-----------|
| **Pfade** | Unix-artige Gruppenpfade innerhalb der HDF5-Datei, beginnend mit `/`. |
| **Zeit** | `timestamps` sind **Sekunden** (Fließkomma), **sample-synchron** zu allen Kanälen (gleiche Länge **N**). |
| **Kanäle** | `channel_0`, `channel_1`, …; Namen auch im Root-Attribut `channels`. |
| **Attribute** | Root (`/`) = gesamtes Fenster; Dataset-Attribute = ein Signal. |

---

## 4. Logischer Standard-Baum (normativ, nur EEG)

```text
/
├── meta/                    # optional: Session, Gerät, Pipeline, IDs
│   ├── acquisition
│   └── identifiers
├── raw/
│   └── eeg/
│       ├── time/
│       │   └── timestamps   # float64, Länge N
│       └── signals/
│           ├── channel_0    # 1D, Länge N
│           └── channel_*    # weitere Kanäle
├── derived/
│   └── eeg/
│       └── …
└── events/
    └── …
