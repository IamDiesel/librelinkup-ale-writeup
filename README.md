# librelinkup-ale-writeup

**[Reverse-Engineering-Writeup](https://github.com/IamDiesel/librelinkup-ale-writeup/blob/main/20260922_LibreLinkUp_RE_Public.pdf) zur doppelten Verschlüsselung von LibreLinkUp (TLS + White-Box-ALE) — ein Erkenntnis-Bericht zur persönlichen Interoperabilität mit den eigenen Glukosewerten. Kein Kochrezept, kein Exploit-Code.**

> ⚠️ **Medizinischer Haftungsausschluss.** Dies ist ein technischer Sicherheits- und Reverse-Engineering-Bericht, **kein medizinisches Dokument**. Die beschriebenen Verfahren und sämtliche damit gewonnenen Glukosewerte (CGM-Daten) dürfen **unter keinen Umständen** für medizinische Entscheidungen herangezogen werden — insbesondere nicht für die Dosierung von Insulin oder andere Therapieanpassungen. Für Therapieentscheidungen sind ausschließlich die vom Hersteller zugelassenen, geprüften Anzeigegeräte und -Apps sowie ärztlicher Rat maßgeblich.

## Worum es geht

LibreLinkUp verschlüsselt seine API-Nutzlast **doppelt**: Einmal per TLS und darüber hinaus noch einmal *innerhalb der App* (Application-Level Encryption, „ALE") mit einer **White-Box-Kryptografie**. Dieser Bericht erklärt die Krypto- und Schutz-Architektur (ALE, White-Box, RASP) und die zwei Wege, den **eigenen** Glukosewert für die **eigene** Smartwatch nutzbar zu machen — motiviert durch persönliche Interoperabilität, falls die offene REST-Schnittstelle wegfällt.

Der Fokus liegt auf **Verständnis und Methodik**. Durchgeführt wurde das gesamte Vorgehen auf einem **ungerooteten** Gerät, ausschließlich mit den **eigenen** Zugangsdaten und Gesundheitsdaten.

## Inhalt

| Datei | Beschreibung |
|---|---|
| `LibreLinkUp_RE_Public_full-1.pdf` | Der vollständige Bericht als PDF — vorangestellter Krypto-Primer („Teil 0") + Hauptbericht. |
| `LibreLinkUp_RE_Public_full.md` | Dieselbe Fassung als Markdown-Quelle. |
| `LICENSE` | Lizenz (CC BY 4.0). |

## Scope, Ethik & bewusste Auslassungen

Diese Veröffentlichung ist ein **Security-/RE-Research-Writeup**. Sie erklärt Architektur, Konzepte und Methodik, damit andere das *Verständnis* nachvollziehen können. Sie enthält **absichtlich nicht**:

- lauffähige Exploit-/Hook-Quelltexte,
- die konkreten Smali-Patches, die den Manipulationsschutz neutralisieren,
- build-spezifische Speicheradressen (Offsets) und Krypto-Konstanten,
- Schlüsselmaterial oder personenbezogene Daten jeglicher Art.

Diese Bausteine würden den Text in ein schlüsselfertiges Werkzeug zur Umgehung des Schutzes einer fremden App verwandeln — das ist nicht das Ziel. Wer denselben Weg für seine eigenen Daten geht, muss die gerätespezifischen Details selbst erarbeiten.

## Zugehöriges Projekt

Die praktische Umsetzung — eine schlanke Android- & Wear-OS-App, die den eigenen Glukosewert liest und auf der Uhr anzeigt — liegt in einem **separaten** Repository:

- **GlucoBridge** — *([GlucoBridge](https://github.com/IamDiesel/GlucoBridge))*

Die Trennung ist bewusst: Hier die Erkenntnisse, dort die (IP-freie) Anwendung.

## Kein Markenbezug / Haftung

„LibreLinkUp", „LibreView" und „FreeStyle Libre" sind Marken ihrer jeweiligen Inhaber. Dieses Repository steht in **keiner** Verbindung zu Abbott und wird von dort weder unterstützt noch geprüft. Alle Analysen erfolgten am eigenen Gerät mit eigenen Daten; jede Nutzung der Informationen geschieht auf eigene Verantwortung.

## Lizenz

© 2026 IamDiesel — lizenziert unter [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).
Bei Weiterverwendung bitte Namensnennung + Link zur Lizenz. Details siehe [`LICENSE`](./LICENSE).
