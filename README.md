# kanzlei-feedback

Fehlerreport-Plugin für die Kanzlei-Skills [`legal-ops-germany`](https://github.com/eliasreiche/legal-ops-germany) und [`tax-ops-germany`](https://github.com/eliasreiche/tax-ops-germany).

Sagt die Nutzerin ausdrücklich „das ist falsch" oder „melde das an Elias", baut Claude einen strukturierten Fehlerbericht **ohne Mandantendaten**, prüft ihn per Regex-Netz (`pruefe_report.py`), zeigt ihn zur Freigabe und schickt ihn erst nach einem ausdrücklichen „Ja" an den Maintainer (Mail-Werkzeug oder `mailto:`-Link). Nichts wird gespeichert.

> Dieses Projekt ist nicht mit Anthropic PBC verbunden. Claude und Anthropic sind Marken der Anthropic PBC.

## Installation

**Claude-App (Abo):** Anpassen → Plugins → Marketplace hinzufügen → Aus einem Repository hinzufügen → `https://github.com/eliasreiche/kanzlei-feedback` → Plugin „kanzlei-feedback" installieren.

**Claude Desktop auf Amazon Bedrock (Drittanbieter-Modus):** Nutzer können dort keine Marketplaces selbst hinzufügen. Der Marketplace kommt über das Verwaltungsprofil (`.mobileconfig`), Schlüssel `allowedPluginMarketplaces`:

```json
{"source":"github","repo":"eliasreiche/kanzlei-feedback","expectedName":"kanzlei-feedback","installationPreference":"available"}
```

Danach erscheint das Plugin unter Einstellungen → Plugins → Organisation.

## Datenschutz

Der Bericht verlässt die Kanzlei. Deshalb gilt eine absolute Sperrliste (Namen, Aktenzeichen, Steuernummern, IBAN, Anschriften, wörtliche Passagen …), ein Whitelist-Aufbau des Berichts, eine zusätzliche Regex-Prüfung und die Sichtfreigabe durch die Nutzerin. Details in [`skills/kanzlei-feedback/SKILL.md`](skills/kanzlei-feedback/SKILL.md).

## Selbsttest

```bash
python3 skills/kanzlei-feedback/pruefe_report.py --demo
```

## Updates

Bei jeder Änderung `version` in `.claude-plugin/plugin.json` heben.

## Lizenz

Siehe [`LICENSE`](LICENSE).
