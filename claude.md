# Projekt



Diese App ist die zentrale Management-Software für ein Gebäudereinigungs- und Gartenpflegeunternehmen und soll schrittweise alle betrieblichen Abläufe digital abbilden. Erstes Kernfeature ist die objektbezogene Zeiterfassung der Mitarbeiter vor Ort, deren Daten als Grundlage für die Rechnungsvorbereitung und später für die Rechnungserstellung und den Versand dienen.

Ausführliche Beschreibung: specs/projekt.md (hier nicht wiederholen).



# Über mich

* Ich bin kein Entwickler. Erkläre in einfacher Sprache, Fachbegriffe in einem Satz.
* Wenn etwas unklar ist: frag, statt zu raten. Immer nur eine Frage auf einmal.
* Architekturentscheidungen (schwer später zu ändern, z. B. Datenmodell, neue Dienste, größere Bibliotheken): nenne mir 2-3 Optionen mit Vor- und Nachteilen und deiner Empfehlung, bevor du umsetzt. Meine Wahl hältst du kurz in specs/entscheidungen.md fest.
* Kleinere Entscheidungen triffst du selbst und nennst sie in der PR-Beschreibung.

# Technik

* Next.js mit TypeScript, Node.js 24
* Hosting: Vercel (EU-Region)
* Datenbank: Supabase (Postgres, EU-Region), Login: Supabase Auth
* Ziel: verbreitete Standardtechnik, für andere Entwickler übernehmbar, Daten jederzeit exportierbar. Nichts Exotisches einführen.

# Umgebung und Datenbank

* Du arbeitest in einer Cloud-Umgebung ohne Docker, also ohne lokale Datenbank.
* Es gibt zwei Datenbanken, je ein eigenes Supabase-Projekt: Stage und Prod.
* Stage ist deine Test-Datenbank. Die Zugangsdaten stehen als Umgebungsvariablen bereit. Alle deine Tests (auch End-to-End) laufen dagegen, ebenso alle Vercel-Vorschauen.
* Prod ist für dich tabu: nicht verbinden, nicht anfassen, keine Production-Umgebungsvariablen. Prod-Zugangsdaten sind absichtlich nicht in deiner Umgebung. Tauchen sie doch auf: nicht benutzen, mir melden.
* Datenbankänderungen nur als Migrationsdateien im Repo. Du wendest sie auf Stage an und testest dort. Auf Prod wende ich sie an, bevor der PR zusammengeführt wird. Weise im PR darauf hin.
* Alle Vorschauen teilen sich die Stage-Datenbank. Darum Datenbank-PRs nacheinander abarbeiten.
* Nur Testdaten, keine echten personenbezogenen Daten. Tests legen ihre Daten selbst an und räumen sie wieder auf.
* Fehlt in der Umgebung etwas (Berechtigung, Internetzugriff, Paket): nicht umgehen, sondern sagen, was fehlt.

# Befehle

* Installieren: npm install
* Tests: npm test
* Build: npm run build
* Migration auf Stage anwenden: \[noch nicht festgelegt, hier eintragen]
* End-to-End-Tests (Playwright): \[noch nicht eingerichtet, hier eintragen, sobald vorhanden]

# Arbeitsweise

* Vor jeder Aufgabe die passende Spec in specs/ lesen.
* Kleinkram (Texte, Layout, Tippfehler, ohne Logik): direkt umsetzen und PR öffnen.
* Alles andere: erst kurzen Plan im Chat vorlegen und auf meine Freigabe warten, dann bauen.
* Ein Branch = eine Aufgabe = ein PR. Nie direkt auf main, das Zusammenführen mache ich. Nichts ändern, was nicht zur Aufgabe gehört.
* Jedes neue Verhalten bekommt einen Test. Abnahmekriterien aus der Spec werden zu Tests.
Kriterien zu Rollen und Zugriffsverboten bekommen zusätzlich einen End-to-End-Test, sobald diese eingerichtet sind. Bis dahin im PR als offen vermerken.
* Vor dem PR müssen Tests und Build erfolgreich sein.
* Weicht die Umsetzung von der Spec ab, oder fehlt etwas, das Verhalten oder Regeln für Nutzer ändert: stopp und frag mich. Kleine Lücken (z. B. Button-Text) entscheidest du selbst und nennst sie im PR.
* End-to-End-Tests einzurichten ist eine eigene Aufgabe mit eigenem PR. Neues Paket, CI-Schritt und nötige Internetfreigaben stehen im Plan. Danach läuft der Test bei jedem PR in der CI, und du trägst den Befehl oben ein.

# Freigaben

**Im Plan nennen** (meine Freigabe des Plans gilt dann als Zustimmung):

* neue Pakete/Abhängigkeiten
* Datenbankschema (als Migrationsdatei im PR)
* Login oder Rechteprüfung
* Änderungen an .github/workflows/

Fällt erst während der Umsetzung auf, dass so etwas nötig ist und es steht nicht im Plan: stopp und frag.

**Nur auf meine ausdrückliche Anweisung, jedes Mal einzeln:**

* Tests löschen, abschwächen oder überspringen
* .env-Dateien anlegen, lesen oder ändern

Alles andere innerhalb der Aufgabe (Code, Tests, Aufräumen in betroffenen Dateien, Texte, Styling, Doku) machst du ohne Nachfrage.

# Sicherheit

* Rechte werden immer auf dem Server geprüft, nicht nur in der Oberfläche.
* Jede Datenbank-Tabelle bekommt Row Level Security (Zugriffsregeln direkt in der Datenbank).
* Alle Nutzereingaben gelten als unsicher und werden geprüft.
* Zugangsdaten nur als Umgebungsvariablen, nie im Code, im Chat oder in PR-Beschreibungen. Der Supabase-Service-Schlüssel darf nie im Browser-Code landen (nie mit NEXT\_PUBLIC\_).
* Keine personenbezogenen Daten in Logs oder Fehlermeldungen.

# Pull Requests

Jede PR-Beschreibung enthält:

1. Was ändert sich für den Nutzer (einfache Sprache)
2. Welche Dateien wurden geändert und warum
3. Wie teste ich es auf der Preview (Schritt für Schritt, Preview-Link aus dem Vercel-Kommentar im PR)
4. Risiken: Berührt der PR Login, Rechte, Datenbank, Abhängigkeiten oder personenbezogene Daten?
5. Bei Migrationen: auf Stage getestet, muss vor dem Zusammenführen noch von mir auf Prod angewendet werden

