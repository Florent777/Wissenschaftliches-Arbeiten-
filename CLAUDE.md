# CLAUDE.md

Behavioral guidelines to reduce common LLM coding mistakes. Merge with project-specific instructions as needed.

**Tradeoff:** These guidelines bias toward caution over speed. For trivial tasks, use judgment.

## Projektkontext

- **Fach:** Wissenschaftliches Arbeiten (FHDW)
- **Thema:** Chancen und Risiken von ETFs für Privatanleger
- **Autoren:** Florent (GitHub: Florent777) und Jerome
- **Umfang:** jeweils 5 Seiten Inhalt pro Person (~10 Seiten Inhalt gesamt; Deckblatt, Verzeichnisse und Anhang zählen nicht mit)
- **Abgabeformat:** Word (.docx)
- **Zusätzlich:** am Ende eine Präsentation der Ergebnisse
- **Zitierstil:** deutsche Zitierweise per Fußnote im FHDW-Format (siehe Abschnitt 6)
- **Sprache der Arbeit:** Deutsch

Diese Datei ist bewusst zweisprachig: Die allgemeinen Basis-Guidelines (Abschnitte 1-4) wurden unverändert übernommen, die projektspezifischen Abschnitte sind auf Deutsch, der Arbeitssprache.

### Repo-Struktur

| Pfad | Zweck |
|---|---|
| `Gliederung.md` | gemeinsame Struktur/Inhaltsverzeichnis inkl. wer welchen Teil schreibt |
| `Status/Fortschritt.md` | Koordinations-Log: wer hat wann was gemacht, offene Fragen, wer bearbeitet gerade welche Datei |
| `Quellen/Literaturverzeichnis.md` | eine gemeinsame Quellenliste für beide Autoren |
| `Entwurf/*.md` | Textentwürfe pro Kapitel in Markdown – hier primär mit den KI-Assistenten am Inhalt arbeiten |
| `Word/` | die eigentlichen .docx-Dateien (Zielformat der Abgabe) |
| `Praesentation/` | Vorbereitung der Abschlusspräsentation |

Warum Markdown-Entwürfe zusätzlich zu Word: Git kann Textänderungen von euch beiden zuverlässig zusammenführen; bei `.docx` geht das nicht (Merge-Konflikte in Word-Dateien lassen sich nicht automatisch auflösen und riskieren Datenverlust). Workflow: Inhalt in `Entwurf/*.md` erarbeiten und abstimmen → fertigen Text in die Word-Datei mit FHDW-Formatvorlage übertragen (inkl. echter Word-Fußnoten).

## 1. Think Before Coding

**Don't assume. Don't hide confusion. Surface tradeoffs.**

Before implementing:
- State your assumptions explicitly. If uncertain, ask.
- If multiple interpretations exist, present them - don't pick silently.
- If a simpler approach exists, say so. Push back when warranted.
- If something is unclear, stop. Name what's confusing. Ask.

## 2. Simplicity First

**Minimum code that solves the problem. Nothing speculative.**

- No features beyond what was asked.
- No abstractions for single-use code.
- No "flexibility" or "configurability" that wasn't requested.
- No error handling for impossible scenarios.
- If you write 200 lines and it could be 50, rewrite it.

Ask yourself: "Would a senior engineer say this is overcomplicated?" If yes, simplify.

## 3. Surgical Changes

**Touch only what you must. Clean up only your own mess.**

When editing existing code:
- Don't "improve" adjacent code, comments, or formatting.
- Don't refactor things that aren't broken.
- Match existing style, even if you'd do it differently.
- If you notice unrelated dead code, mention it - don't delete it.

When your changes create orphans:
- Remove imports/variables/functions that YOUR changes made unused.
- Don't remove pre-existing dead code unless asked.

The test: Every changed line should trace directly to the user's request.

## 4. Goal-Driven Execution

**Define success criteria. Loop until verified.**

Transform tasks into verifiable goals:
- "Add validation" → "Write tests for invalid inputs, then make them pass"
- "Fix the bug" → "Write a test that reproduces it, then make it pass"
- "Refactor X" → "Ensure tests pass before and after"

For multi-step tasks, state a brief plan:
```
1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]
```

Strong success criteria let you loop independently. Weak criteria ("make it work") require constant clarification.

*Anwendung auf diese Arbeit:* „Code" → Text/Argumentation, „Tests" → Quellenbeleg/Plausibilitätsprüfung, „Refactoring" → Umformulieren, „Bug" → sachlicher/inhaltlicher Fehler oder falsches Zitat.

## 5. Koordination zwischen mehreren Personen/KI-Sessions

Florent und Jerome arbeiten unabhängig (an unterschiedlichen Rechnern, ggf. mit unterschiedlichen Chatbots) an diesem Repo. Damit alle Sessions abgestimmt bleiben, gilt für jede Session verbindlich:

1. **Vor der Arbeit:** `git pull`, dann `Status/Fortschritt.md` und `Gliederung.md` lesen, um den aktuellen Stand zu kennen, bevor irgendetwas geändert wird.
2. **Vor dem Bearbeiten einer `.docx`-Datei:** in `Status/Fortschritt.md` eintragen, wer die Datei gerade bearbeitet – nie gleichzeitig an derselben Word-Datei arbeiten (siehe `Word/README.md`).
3. **Während der Arbeit:** neue Quellen sofort in `Quellen/Literaturverzeichnis.md` eintragen (verhindert doppelte/inkonsistente Zitate zwischen den beiden Teilen).
4. **Nach der Arbeit:** Änderung kurz in `Status/Fortschritt.md` protokollieren (Datum, Person, was geändert, offene Fragen), committen mit aussagekräftiger Message.
5. **Nicht automatisch pushen oder Konflikte einfach überschreiben.** Bei Unsicherheit oder Merge-Konflikt: beide Versionen dem Nutzer zeigen und Rückfrage stellen statt zu raten.

## 6. Zitierstil & fachliche Sorgfalt (worauf die KI aktiv hinweisen soll)

**Zitierstil (FHDW-Standard, verbindlich).** Fußnote:
```
1 Nachname, Vorname (Jahr), S. XX f.
1 Nachname, Vorname (Jahr), Titel, S. XX f.
1 Nachname, V. (Jahr), S. XX f.
1 Nachname, V. (Jahr), Titel, S. XX f.
```
„f." = die folgende Seite auch gemeint, „ff." = mehrere folgende Seiten. Innerhalb einer Quelle einheitlich bleiben (nicht mal abgekürzt, mal ausgeschrieben). Vollständiges Literaturverzeichnis-Format ist mit der Lehrkraft noch nicht bestätigt (siehe `Quellen/Literaturverzeichnis.md`).

**Aktiv prüfen und ansprechen, nicht stillschweigend ignorieren:**
- Unbelegte Behauptungen: jede Zahl/Tatsachenbehauptung braucht eine Fußnote; keine Quelle erfinden.
- Fußnoten ↔ Literaturverzeichnis: jede Fußnote muss einen passenden Eintrag in `Quellen/Literaturverzeichnis.md` haben und umgekehrt.
- Quellenqualität: jede neue Quelle nach dem Bewertungsschema in `Quellen/Literaturverzeichnis.md` einstufen (Lehrbuch/Herausgeberwerk/Fachzeitschrift/Arbeitspapier, angepasst um Aktualität & Seriosität); bei überwiegend niedrig bewerteten oder veralteten Quellen aktiv warnen und bessere Alternativen vorschlagen.
- Word-Fußnoten technisch korrekt setzen: immer Words automatische Fußnotenfunktion verwenden, niemals Nummern von Hand eintippen – sonst verschieben sich beim Zusammenführen der beiden Teile alle Nummern.
- Konsistenz zwischen den beiden Teilen (Florent/Jerome): gleiche Begriffe/Abkürzungen einheitlich verwenden, keine Widersprüche zwischen Chancen- und Risiken-Teil, keine doppelt erklärten Grundlagen.
- Seitenzahl im Blick behalten: ~5 Seiten Inhalt pro Person – bei deutlicher Über-/Unterschreitung aktiv ansprechen.

**Fachliche Sorgfalt beim Thema ETF** – erfahrungsgemäß häufige Fehler, aktiv gegenprüfen statt unreflektiert übernehmen:
- TER/Kostenquote ist nicht identisch mit den Gesamtkosten (Spread, Tracking Difference kommen hinzu) – Tracking Error ≠ Tracking Difference.
- ETFs sind als Sondervermögen insolvenzgeschützt – uneingeschränkt bei physischer Replikation; bei synthetischer Replikation besteht ein (meist besichertes) Kontrahentenrisiko aus dem Swap-Geschäft. Diese Unterscheidung wird oft zu stark vereinfacht.
- Diversifikation reduziert unsystematisches Risiko, eliminiert aber nicht das allgemeine Marktrisiko.
- Besteuerung (Vorabpauschale, Teilfreistellung, Sparer-Pauschbetrag) korrekt und aktuell darstellen, nicht die Rechtslage vor der Investmentsteuerreform 2018.
- Begriffe nicht vermischen: ETF ≠ Zertifikat ≠ klassischer aktiv gemanagter Fonds.
- Alle Markt-/Kostenzahlen (Marktvolumen, Anzahl ETFs, Beispiel-TER) mit Quelle und Datum versehen, nicht aus dem Gedächtnis schätzen.
- Regulatorischen Rahmen korrekt benennen (OGAW/UCITS-Richtlinie, PRIIPs-Verordnung/Basisinformationsblatt).

Diese Liste ersetzt keine Quellenprüfung – sie soll nur verhindern, dass verbreitete Vereinfachungen unreflektiert übernommen werden. Bei Unsicherheit: als offene Frage in `Status/Fortschritt.md` markieren statt zu raten.

---

**These guidelines are working if:** fewer unnecessary changes in diffs, fewer rewrites due to overcomplication, and clarifying questions come before implementation rather than after mistakes.
