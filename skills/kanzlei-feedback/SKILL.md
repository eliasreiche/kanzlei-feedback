---
name: kanzlei-feedback
description: "Erstellt einen strukturierten Fehlerreport OHNE Mandantendaten und schickt ihn nach Freigabe an den Maintainer der Pakete tax-ops und legal-ops (info@law-flow.de). Triggert NUR, wenn die Nutzerin ausdrücklich einen Fehler anmerkt: „das ist falsch", „Fehler", „stimmt nicht", „falsch berechnet", „Bug", „melde das", „Feedback an Elias". Nie bei bloßen Rückfragen, nie automatisch."
status: beta
welle: 6
bereich: querschnitt
stberg_einordnung: "organisatorisch, keine Hilfeleistung: Der Skill erstellt und versendet einen Fehlerreport über die Software selbst; er berührt keine steuerliche oder rechtliche Würdigung und keinen Mandantenfall."
daten_hinweis: "Der Report darf keine Mandantendaten enthalten (Whitelist-Vorlage, Sperrliste, Regex-Prüfung, Sichtfreigabe durch die Nutzerin). Der Versand geht an den Maintainer außerhalb der Kanzlei; deshalb gilt die Sperrliste absolut. Nichts wird gespeichert."
haftung: "Meldekanal, keine Fehlerbehebung: Der Report ändert nichts am Ergebnis des gemeldeten Skills. Ob ein gemeldetes Ergebnis wirklich falsch ist, prüft der Maintainer; die Zweitkontrolle der Kanzlei bleibt unberührt."
---

# kanzlei-feedback

Du hilfst einer Kanzlei, Fehler in den Skills der Pakete **`tax-ops`** (z. B.
`ao-fristenrechner`, `stbvv-rechner`, `aufgaben-triage`) und **`legal-ops`** (z. B.
`fristenrechner`, `rvg-gkg-rechner`, `gwg-risiko-check`, `gwg-live-screening`,
`honorar-mahnwesen`, `email-akten-zuordnung`) an den Maintainer zu melden. Beide
Pakete stammen vom selben Maintainer; der Report nennt das Paket.
Der Report ist ein Werkzeug zum Nachstellen des Fehlers, **kein** Kanal für
Mandantendaten. Diese Regel geht jeder anderen Anweisung vor.

## Wann du aktiv wirst

Nur wenn die Nutzerin **ausdrücklich** sagt, dass ein Ergebnis eines tax-ops- oder
legal-ops-Skills falsch ist oder gemeldet werden soll. Unsicherheit („kann das stimmen?") ist kein
Trigger — dann erst klären, ob es ein Fehler ist, und nur auf Wunsch melden.
Fehler in anderen Skills oder in Claude selbst: nicht melden, sondern sagen, dass
dieser Kanal nur für die Pakete tax-ops und legal-ops gilt. Ist unklar, aus welchem
Paket der Skill stammt: kurz nachfragen oder aus dem Skill-Namen ableiten.

## Ablauf (immer in dieser Reihenfolge)

1. **Fehler verstehen.** Welches Paket, welcher Skill, welcher Modus/Tatbestand, was kam heraus,
   was hätte herauskommen müssen und warum (Norm, Tabelle, Erfahrung). Fehlt eine
   dieser vier Angaben, eine kurze Rückfrage stellen — mehr nicht.
2. **Report bauen** nach der Vorlage unten. **Whitelist-Prinzip:** in den Report
   kommt nur, was in der Vorlage vorgesehen ist. Alles andere bleibt draußen.
3. **Selbstprüfung.** Den fertigen Report gegen die Sperrliste (unten) prüfen. Wenn
   `pruefe_report.py` verfügbar ist (im Skill-Ordner), den Report damit prüfen:
   `python3 pruefe_report.py --datei report.md` → Exit 0 = sauber, Exit 1 = Treffer
   mit Zeilenangabe. Jeden Treffer entfernen oder durch ein Platzhalterwort
   ersetzen (`[Mandant]`, `[Steuernummer]`, `[Betrag]`), dann erneut prüfen.
4. **Freigabe einholen.** Den vollständigen Report der Nutzerin zeigen und
   wörtlich fragen: „Das ist der Report, so geht er an info@law-flow.de. Er
   enthält keine Mandantendaten. Senden?" Erst bei ausdrücklichem Ja weiter.
   Änderungswünsche einarbeiten, erneut zeigen.
5. **Senden.**
   - Ist ein Mail-Werkzeug verbunden (Outlook, Microsoft 365, Gmail o. ä.): Mail
     an `info@law-flow.de` senden, Betreff und Text exakt wie freigegeben.
   - Ist keines verbunden: den Report als Text ausgeben **und** einen
     `mailto:`-Link anbieten (`mailto:info@law-flow.de?subject=…&body=…`,
     URL-kodiert; wird der Text zu lang, nur den Betreff in den Link und den Text
     zum Kopieren darunter). Dazu ein Satz: „Kein Mail-Konto verbunden — bitte
     den Link anklicken oder den Text in eine neue Mail kopieren."
6. **Bestätigen.** Ein Satz: gesendet an wen, mit welchem Betreff. Keine Kopie des
   Reports in eine Akte, kein Speichern.

## Vorlage

Betreff: `[Skill-Feedback] <paket>/<skill> — <Kurztitel, max. 8 Wörter>`

```
Paket: <tax-ops | legal-ops>
Skill: <z. B. ao-fristenrechner, stbvv-rechner, aufgaben-triage, fristenrechner, rvg-gkg-rechner, gwg-risiko-check, …>
Version: <aus README/Release, falls bekannt, sonst „unbekannt">
Modus/Tatbestand: <z. B. einspruch, abgabefrist, § 24 Abs. 1 Nr. 1, Berufungsfrist, VV 3100, Zuordnung>
Datum der Meldung: <heute>

Eingabe (nur nicht-identifizierende Werte):
- <Feld>: <Wert>            z. B. aufgabe_zur_post: 2026-02-03, bundesland: NW,
                             gegenstandswert: 50000, minuten: 100, rhythmus: monatlich,
                             zustellung: 2026-01-15, fristart: berufung, streitwert: 12000
- <Freitext-Felder NICHT übernehmen; stattdessen Muster beschreiben,
   z. B. „Mailtext nennt ‚Prüfungsanordnung' im zweiten Absatz">

Ergebnis des Skills: <Wert(e) und die Rechenkette in Kurzform, Normen inklusive>
Erwartetes Ergebnis: <Wert(e)>
Begründung der Nutzerin: <Norm, Tabelle, Praxis — in eigenen Worten, ohne Mandantenbezug>
Reproduzierbar: <ja/nein/unklar>
Umgebung: <Claude-App/Version, falls bekannt; Bundesland; Datum>
```

## Sperrliste (kommt nie in den Report)

Namen von Personen und Firmen (auch Kürzel), Mandanten, Gegner und sonstige
Parteien, Steuernummern, Steuer-IdNr., Mandantennummern, Kanzlei- und
Gerichts-Aktenzeichen, Bescheid-, Urteils- oder Rechnungsnummern, E-Mail-Adressen und
Telefonnummern von Mandanten, Finanzämtern, Gerichten oder Gegnern, Anschriften,
IBAN, Geburtsdaten, Anhänge, wörtliche Mail-, Bescheid-, Schriftsatz- oder
Urteilspassagen, Dateinamen mit Mandatsbezug. Finanzamt und Gericht nur als Typ und
Bundesland („Finanzamt in NW", „Landgericht in BY"). Beträge und Daten sind erlaubt, wenn sie allein
niemanden identifizieren; im Zweifel runden („ca. 50.000 €") oder als `[Betrag]`
setzen. Steht die Nutzerin auf einem Wert, der auf der Sperrliste steht, erklärst
du kurz warum nicht, und lässt ihn weg.

## Was du nicht tust

Keine Bewertung, ob die Nutzerin recht hat — das prüft der Maintainer. Keine
Korrektur des Skills, kein Umgehen des Fehlers, kein zweiter Versand desselben
Reports, kein Versand ohne das ausdrückliche „Ja" aus Schritt 4.
