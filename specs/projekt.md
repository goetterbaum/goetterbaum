# Projekt: Firmen-App Gebäudereinigung \& Gartenpflege

## Ziel

* Zentrale Management-App für ein Gebäudereinigungs- und Gartenpflegeunternehmen, die schrittweise alle betrieblichen Abläufe digital abbildet.
* Für die Firmenleitung bzw. das Büro (Verwaltung, Abrechnung) und für die Mitarbeiter im Außendienst (Zeiterfassung am Objekt).
* Die App hat sich gelohnt, wenn:

  * Arbeitszeiten nicht mehr auf Papier oder per Zuruf erfasst werden, sondern direkt am Objekt per App.
  * die Rechnungsvorbereitung aus den erfassten Zeiten deutlich schneller und mit weniger Fehlern geht.
  * jederzeit nachvollziehbar ist, wer wann wie lange an welchem Objekt gearbeitet hat.

## Nutzer und Rollen

(Verbindliche Rollenliste. Feature-Specs verweisen darauf. Vorschlag, noch zu bestätigen.)

* **Admin / Inhaber**: darf alles, inkl. Benutzer, Rollen, Stammdaten, Rechnungen und Einstellungen verwalten.
* **Büro / Verwaltung**: verwaltet Kunden, Objekte und Mitarbeiter, sieht und korrigiert alle Zeiteinträge, bereitet Rechnungen vor.
* **Mitarbeiter (Außendienst)**: sieht die ihm zugeordneten Objekte, erfasst seine eigenen Zeiten, sieht nur seine eigenen Einträge.
* *(Optional)* **Vorarbeiter / Objektleiter**: sieht und bestätigt die Zeiten seines Teams.

## Funktionsübersicht

Geplante Features in grober Reihenfolge. Jedes bekommt eine eigene Feature-Spec.

1. **Objektverwaltung**: Objekte (Einsatzorte) mit Adresse, Kunde, Leistungsart (Reinigung, Garten) und Einnahmen pro Objekt anlegen und pflegen.
2. **Mitarbeiterverwaltung**: Mitarbeiter anlegen, Rollen vergeben, Objekte zuordnen, die Kosten pro Arbeitsstunde (Lohn inkl. Nebenkosten), die vereinbarten Wochenstunden und die daraus folgenden Tagessollstunden hinterlegen.
3. **Zeiterfassung am Objekt**: Mitarbeiter wählt in der App das Objekt und startet bzw. stoppt die Arbeitszeit vor Ort; Wegezeiten zwischen den Objekten werden mit erfasst.
4. **Zeitübersicht und Freigabe**: Büro sieht alle Zeiten je Mitarbeiter und Objekt, kann korrigieren und freigeben.
5. **Wirtschaftlichkeitsanalyse**: zeigt aus Einnahmen, Arbeits- und Wegezeiten sowie Mitarbeiterkosten, wie viel Gewinn pro Objekt und pro Arbeitstag eines Mitarbeiters übrig bleibt, und markiert kritische Objekte, z. B. wegen zu langer Wegezeiten.
6. **Lohnabrechnungsvorbereitung**: erfasst Urlaub, Krankheit und Feiertage, erstellt aus den freigegebenen Zeiten je Mitarbeiter eine Monatsübersicht mit Ist- und Soll-Stunden, führt Über- und Unterstunden fort und erzeugt eine Excel-Tabelle für das externe Lohnabrechnungsbüro.
7. **Rechnungsvorbereitung**: freigegebene Zeiten je Kunde, Objekt und Zeitraum zusammenfassen als Grundlage für die Rechnung.
8. **Rechnungserstellung und Versand**: Rechnungen direkt aus der App erstellen und an Kunden versenden.

Spätere Ideen (noch nicht priorisiert): Kundenverwaltung, Einsatz- und Tourenplanung, Leistungsnachweise mit Fotos, Urlaubs- und Abwesenheitsverwaltung, Material- und Geräteverwaltung.

## Daten (Überblick)

* **Arten von Daten**: Mitarbeiter, Kunden, Objekte, Zeiteinträge (Arbeits- und Wegezeiten), Leistungsarten, Einnahmen pro Objekt, Kosten pro Mitarbeiterstunde, Wochen- und Tagessollstunden, Abwesenheiten (Urlaub, Krankheit, Feiertage), Stundenkonten (Über- und Unterstunden), Lohnexporte (Excel), später Rechnungen.
* **Personenbezogen**:

  * Mitarbeiterdaten (Name, Kontakt, Rolle, Lohn bzw. Kosten pro Stunde, Soll-Stunden)
  * Abwesenheiten; Krankheitstage sind besonders sensibel (nur „krank“ mit Datum, keine Diagnosen speichern)
  * Stundenkonten und Lohnexporte (gehen an das externe Lohnabrechnungsbüro)
  * Zeiteinträge (Arbeitszeiten, ggf. Standort beim Ein- und Ausstempeln)
  * Ansprechpartner der Kunden
* **Wer darf was sehen**:

  * Mitarbeiter sehen nur ihre eigenen Zeiteinträge, ihr eigenes Stundenkonto und ihre zugeordneten Objekte.
  * Büro und Admin sehen alle Daten.
  * Einnahmen, Rechnungsdaten und Auswertungen sehen nur Büro und Admin.
  * Löhne bzw. Kosten pro Mitarbeiterstunde sieht nur der Admin (zu entscheiden, ob auch das Büro).

## Regeln, die überall gelten

* Jeder Zeiteintrag gehört genau zu einem Mitarbeiter und einem Objekt.
* Zeiten werden mit Beginn und Ende erfasst, die Dauer wird daraus berechnet.
* Korrekturen an Zeiteinträgen werden protokolliert (wer, wann, was geändert), der Originalwert bleibt nachvollziehbar.
* Nur freigegebene Zeiten fließen in die Rechnungsvorbereitung, die Wirtschaftlichkeitsanalyse und die Lohnabrechnungsvorbereitung ein.
* Tagessollstunden ergeben sich aus den Wochenstunden des Mitarbeiters (z. B. 40 Wochenstunden = 8 Stunden pro Arbeitstag).
* An Feiertagen, Urlaubs- und Krankheitstagen werden dem Mitarbeiter seine Tagessollstunden als Ist-Stunden gutgeschrieben.
* Über- bzw. Unterstunden eines Monats = Ist-Stunden (gearbeitete Zeit plus Gutschriften) minus Soll-Stunden; der Saldo wird fortlaufend in den Folgemonat übertragen.
* Ein Monat wird nach dem Lohnexport abgeschlossen; spätere Korrekturen sind nur noch nachvollziehbar und gekennzeichnet möglich.
* Gewinn = Einnahmen minus Personalkosten (Arbeitszeit plus Wegezeit mal Kosten pro Stunde). Wegezeiten werden dem Objekt zugerechnet, zu dem gefahren wird (Vorschlag, noch zu bestätigen).
* Ein Objekt gilt als kritisch, wenn der Gewinn unter einer festgelegten Grenze liegt oder der Anteil der Wegezeit zu hoch ist (Grenzwerte noch festzulegen).
* Aufzeichnungspflichten beachten: Die Gebäudereinigung unterliegt besonderen Pflichten zur Arbeitszeitdokumentation (Beginn, Ende, Dauer). Konkrete Anforderungen und Aufbewahrungsfristen rechtlich prüfen lassen.
* Noch festzulegen: Pausenregelung, Rundung von Zeiten, Umgang mit vergessenem Ausstempeln, mehrere Objekte pro Tag.

## Technik und Rahmenbedingungen

* **Nutzung**: Mobile-first, da Mitarbeiter die App auf dem Handy am Objekt nutzen. Büro-Funktionen auch am Desktop.
* **Offline**: wünschenswert, da an manchen Objekten schlechter Empfang sein kann (noch zu entscheiden).
* **Stack**: noch offen.
* **Hosting**: in der EU, DSGVO-konform.
* **Umgebungen**: Stage, Prod.
* **Architekturentscheidungen**: werden kurz hier festgehalten, Details in `specs/entscheidungen.md`.

## Nicht dazu gehört

* Keine eigentliche Lohn- und Gehaltsabrechnung (Brutto/Netto, Steuern, Sozialabgaben, Lohnzettel). Die App bereitet nur vor und liefert die Exportdatei, abgerechnet wird beim externen Lohnabrechnungsbüro.
* Keine vollständige Finanzbuchhaltung.
* Kein dauerhaftes GPS-Tracking der Mitarbeiter, höchstens ein Standort-Zeitstempel beim Ein- und Ausstempeln (falls überhaupt).

## Bedingungen für den Go-live

* Rollen und Rechte sind getestet: Mitarbeiter sehen nur ihre eigenen Daten.
* Datenschutz geklärt: Datenschutzinformation für Mitarbeiter, Auftragsverarbeitungsvertrag mit dem Hoster.
* Regelmäßige Backups eingerichtet und Wiederherstellung einmal getestet.
* Zeiterfassung im Praxistest an mindestens einem echten Objekt erprobt.
* Rechtliche Anforderungen an die Arbeitszeitaufzeichnung geprüft.

## Offene Fragen

* Welche Rollen gibt es tatsächlich (z. B. Vorarbeiter)?
* Wie viele Mitarbeiter und Objekte gibt es ungefähr?
* Abrechnung nach Stunden, pauschal pro Objekt oder gemischt? (bestimmt, wie Einnahmen pro Objekt hinterlegt werden)
* Wie werden Wegezeiten erfasst: automatisch als Lücke zwischen zwei Objekten oder per eigenem „Fahrt“-Eintrag?
* Sollen neben Personalkosten weitere Kosten in die Analyse einfließen (Fahrzeug, Material, Gemeinkosten)? Ohne diese ist das Ergebnis ein Deckungsbeitrag, noch kein echter Reingewinn.
* Ab welchem Gewinn oder Wegezeitanteil gilt ein Objekt als kritisch?
* Welche Spalten muss die Excel-Tabelle für das Lohnbüro enthalten? Am besten eine bisherige Tabelle als Vorlage nehmen.
* Zählen Wegezeiten für die Lohnabrechnung als Arbeitszeit?
* Auf welche Tage verteilen sich die Wochenstunden (z. B. Mo–Fr), und gibt es Mitarbeiter mit ungleichmäßig verteilten Arbeitstagen?
* Für welches Bundesland gelten die Feiertage, und sollen sie automatisch hinterlegt werden?
* Wer trägt Urlaub und Krankheit ein: das Büro, oder beantragen die Mitarbeiter Urlaub selbst in der App?
* Gibt es unterschiedliche Beschäftigungsarten (Vollzeit, Teilzeit, Minijob) mit eigenen Regeln für Über- und Unterstunden?
* Werden Zuschläge benötigt (Nacht, Sonntag, Feiertag)?
* Soll beim Ein- und Ausstempeln der Standort geprüft werden?
* Muss die App offline funktionieren?
* Welcher Tech-Stack und welches Hosting?
* Welche Anforderungen gelten später für Rechnungen (Format, E-Rechnung, Anbindung an Steuerberater bzw. Buchhaltungssoftware)?

