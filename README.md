# Awards-Netzwerk – Codebuch

Dieses Repository dokumentiert einen Datensatz zum Erkunden von Zusammenhängen zur
Netzwerkvisualisierung von Film- und Fernsehpreisen
(Golden Globes, Emmys, Oscars).

Der Datensatz wurde für einen Pretest im Bereich
Netzwerkanalyse erstellt und ist für die Nutzung
mit dem Tool Palladio vorgesehen.

---

## Forschungsinteresse

Ziel des Projekts ist es, Zusammenhänge zwischen früheren Auszeichnungen
bei den Golden Globes und Emmys und späteren Oscar-Nominierungen
sichtbar zu machen.

Im Mittelpunkt steht dabei die Frage, ob sich zunehmende Bekanntheit
über mehrere Award-Formate hinweg beobachten lässt.

---

## Hypothese

**H1 – Matthäus-Effekt**

Personen, die in früheren Jahren eine Anerkennung durch die
Golden Globes oder die Emmys erhalten haben (Nominierung oder Gewinn),
weisen eine höhere Wahrscheinlichkeit auf, zu einem späteren Zeitpunkt für einen
Oscar nominiert zu werden.

---

## Datengrundlage

- **Zeitraum:** 2022–2024
- **Awards:** Golden Globes, Emmys, Oscars
- **Analyseeinheit:** Beziehung zwischen Person und Award-Ereignis
- **Datentyp:** Netzwerkdaten (Edge- und Node-Listen)

Die Daten basieren auf öffentlich zugänglichen Informationen zu
Nominierungen und Auszeichnungen.

---

## Datenstruktur

### Edge-Liste (`edges.csv`)

Jede Zeile beschreibt eine Beziehung zwischen einer Person und einem
konkreten Award-Ereignis in einem bestimmten Jahr.

**Variablen:**

| Variable | Beschreibung |
|--------|--------------|
| `from` | Name der ausgezeichneten oder nominierten Person |
| `to` | Award-Ereignis inkl. Jahr (z. B. *Oscars 2024*) |
| `year` | Jahr des Award-Ereignisses (Filtervariable) |
| `award` | Art der Auszeichnung (*Oscars*, *Emmys*, *Golden Globe*) |
| `weight` | 1= nominiert, 2= gewonnen |

---

### Node-Liste (`nodes.csv`)

Die Node-Liste enthält Metadaten zu allen Knoten im Netzwerk.

**Variablen:**

| Variable | Beschreibung |
|--------|--------------|
| `id` | Eindeutige Kennung des Knotens |
| `type` | Knotentyp (*Person* oder *AwardEvent*) |
| `label` | Anzeigename des Knotens |

---

## Modellierungsentscheidungen

- Award-Shows werden als **jahresspezifische Ereignisse** modelliert
  (z. B. *Oscars 2024*), um doppelte Kanten zu vermeiden.
- Das Jahr wird zusätzlich als eigene Variable gespeichert, um eine
  zeitliche Filterung in Palladio zu ermöglichen.
- Mehrfache Nominierungen oder Auszeichnungen werden über die Variable
  `weight` definiert.

---

## Verwendung in Palladio

- `edges.csv` wird als Network/Graph geladen
- `source` = Source Node
- `target` = Target Node
- `weight` kann als Edge Weight genutzt werden
- `year` dient der zeitlichen Filterung
- `nodes.csv` kann optional ergänzt werden, um Knotentypen zu unterscheiden

---

## Nutzungskontext

Der Datensatz dient der Analyse zum Erkunden von Zusammenhängen und Visualisierung und
ermöglicht keine kausalen Aussagen.
