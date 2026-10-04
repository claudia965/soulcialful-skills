---
name: anti-ki-floskel
description: Prüft einen Text auf KI-Floskeln und typische KI-Tells (LinkedIn/Instagram flaggen sie als KI-generiert) und schreibt die markierten Stellen menschlich um. Trigger bei "/anti-ki", "KI-Floskeln checken", "ist das zu KI", "klingt das nach KI", "entfloskeln", "floskel-check", "anti-ki-pass", oder wenn ein Text (Caption, Post, Blog, Mail, LinkedIn) auf KI-Textur geprüft werden soll. Zeigt WAS die Floskel ist, WARUM sie auffällt und liefert eine entschärfte Umschreibung.
---

# Anti-KI-Floskel-Checker

Ein Text-Detektor + Umschreiber. Nimmt einen beliebigen Text (Caption, LinkedIn-Post, Blog, Newsletter, Mail) und findet die Stellen, die nach KI klingen — dann schreibt er sie so um, dass sie nach Mensch klingen.

**Kernidee:** KI-Slop hat wiederkehrende Muster. Wer sie kennt, erkennt und ersetzt sie systematisch. Dieser Skill trägt die vollständige Musterliste in [`references/regeln.md`](references/regeln.md) — dort steht jedes Muster mit Beispiel, Grund und Fix.

---

## Ablauf

### 1. Text einlesen
Nimm den Text, den die Nutzerin einfügt oder als Datei nennt. Wenn kein Text da ist, frag: *"Füg den Text ein, den ich checken soll."* Frag außerdem einmalig nach der **Anrede** (Du oder Sie) und ob es **Instagram/LinkedIn/Blog/Mail** ist — das ändert, was als Floskel zählt (z. B. Denglisch ist auf IG okay, in einer Anwalts-Mail nicht).

### 2. Regeln laden
Lies **immer zuerst** [`references/regeln.md`](references/regeln.md). Dort stehen:
- die **8 AI-Tells** (Struktur-Muster),
- die **6 Bait-Pattern A–F** (die Plattformen aktiv als KI flaggen),
- die **harten Form-Regeln** (Gedankenstriche = Hard-No, Nie-Wörter, KI-Füllwörter),
- die **Humanisieren-Checkliste** (Aktiv statt Passiv, Satzlängen mischen, Pronomen, Anekdote, Laut-vorlesen-Test),
- die **bevorzugten Alternativen** (womit man ersetzt).

### 3. Scannen und markieren
Geh den Text Satz für Satz durch. Für **jede** gefundene Stelle notiere:
- **Zitat** — die konkrete Textstelle (kurz, wörtlich).
- **Typ** — welches Muster (z. B. „AI-Tell #3: Umfassende Lösung", „Pattern B: Zerstückelung", „Gedankenstrich", „Füllwort: letztendlich").
- **Warum** — ein Satz, warum es nach KI klingt.
- **Fix** — konkret umgeschrieben in menschlich, in der gewählten Anrede.

Markiere **jeden Gedankenstrich (–, —) einzeln** — das ist ein Hard-No, keine Ausnahme (außer echten Bis-Strichen in Zahlenspannen wie „10–12 Uhr"). Prüf den Text außerdem gegen die **Humanisieren-Checkliste**: durchgehend Passiv? Immer gleich lange Sätze? Kein „ich/du"? Keine einzige Anekdote? Jeder dieser Punkte ist ein eigener Treffer.

Gib das als **Tabelle** aus (Zitat | Typ | Warum | Fix). Sortiere die auffälligsten zuerst.

### 4. Score + Gesamturteil
Zähl die Treffer und gib eine kurze Einordnung:
- **0–1 Treffer** → „Klingt menschlich. Geht raus."
- **2–4 Treffer** → „Ein paar Stellen riechen nach KI. Fix drüber, dann passt's."
- **5+ Treffer** → „Zu glatt. Das flaggt LinkedIn/Instagram als KI. Ich schreib's um."

Sei ehrlich, nicht nett — ein falsches „passt schon" kostet Reichweite.

### 5. Umschreiben (auf Wunsch oder ab 5+ Treffern automatisch anbieten)
Liefere eine **entschärfte Vollversion** des Textes: gleiche Aussage, gleiche Länge grob, aber alle markierten Stellen ersetzt. Halte dich an die **bevorzugten Alternativen** und die **Humanisieren-Checkliste** aus der Regel-Datei: aktiv statt passiv, Satzlängen mischen, „ich/du" statt „man", konkrete Zahlen statt Adjektive, eine Person statt „egal ob X, Y oder Z", fließende Sätze statt Zerstückelung, keine Gedankenstriche. Lies die Umschreibung zum Schluss innerlich **laut** — stolperst du oder klingt es monoton, brich den Rhythmus. **Erfinde keine Fakten** — wenn eine Stelle eine konkrete Zahl oder Anekdote bräuchte, die du nicht hast, setz `[hier deine echte Zahl/Story]` als Platzhalter statt etwas zu halluzinieren.

---

## Wichtige Prinzipien

- **Nur markieren, was wirklich ein Muster ist.** Nicht jeden Satz zerpflücken. Ein Text darf Charakter haben — Ziel ist, KI-*Textur* zu entfernen, nicht die Stimme glattzubügeln.
- **Kontext schlägt Regel.** Denglisch, kleine Rechtschreib-Lockerheit, ein Knallsatz — das ist auf Social erlaubt und oft gewollt. Als KI-Tell zählt nur das *künstliche* davon (siehe Pattern D in der Regel-Datei: Fake-Authentizität).
- **They-Say-But mit konkretem Beispiel ist GUT.** Nur die abstrakte „Es geht nicht um X, sondern um Y"-Variante ohne Beispiel ist die Floskel.
- **Anrede konsequent halten** — was du umschreibst, bleibt durchgehend Du oder Sie.

---

## Output-Vorlage

```
## KI-Check: <Titel/erste Worte des Textes>

**Urteil:** <ein Satz + Treffer-Zahl>

| Zitat | Typ | Warum | Fix |
|---|---|---|---|
| … | … | … | … |

## Entschärfte Version
<voller umgeschriebener Text — nur wenn gewünscht / ab 5+ Treffern>
```
