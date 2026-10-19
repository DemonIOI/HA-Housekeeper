<p align="center"><em><a href="#english">English</a> · <a href="#deutsch">Deutsch</a> · Русская версия: <a href="README.md">README.md</a></em></p>

<a id="english"></a>
<p align="center">
  <img src="https://raw.githubusercontent.com/bertel2020/HA-Housekeeper/main/custom_components/ha_housekeeper/brand/logo.png" alt="HA Housekeeper" width="160">
</p>

<h1 align="center">HA Housekeeper</h1>

<p align="center">
  Maintenance and analysis for Home Assistant: inventory, diagnostics, and dependencies at a glance.
</p>

<p align="center">
  <a href="https://github.com/hacs/integration"><img src="https://img.shields.io/badge/HACS-Custom-41BDF5.svg" alt="HACS Custom"></a>
  <a href="https://www.home-assistant.io/"><img src="https://img.shields.io/badge/Home%20Assistant-Custom%20Integration-18BCF2.svg?logo=home-assistant&logoColor=white" alt="Home Assistant"></a>
  <a href="https://github.com/bertel2020/HA-Housekeeper/releases"><img src="https://img.shields.io/github/v/release/bertel2020/HA-Housekeeper?sort=semver&include_prereleases" alt="Release"></a>
  <a href="https://github.com/bertel2020/HA-Housekeeper/actions/workflows/validate.yml"><img src="https://github.com/bertel2020/HA-Housekeeper/actions/workflows/validate.yml/badge.svg" alt="Validate"></a>
  <a href="LICENSE"><img src="https://img.shields.io/github/license/bertel2020/HA-Housekeeper" alt="License"></a>
</p>

<p align="center">
  <a href="https://buymeacoffee.com/bertel2020"><img src="https://img.shields.io/badge/Buy%20Me%20a%20Coffee-support-FFDD00?logo=buy-me-a-coffee&logoColor=black" alt="Buy Me a Coffee"></a>
  <a href="https://ko-fi.com/bertel2020"><img src="https://img.shields.io/badge/Ko--fi-support-FF5E5B?logo=ko-fi&logoColor=white" alt="Ko-fi"></a>
  <a href="https://paypal.me/RobertoMartins"><img src="https://img.shields.io/badge/PayPal-donate-00457C?logo=paypal&logoColor=white" alt="PayPal"></a>
</p>

HA Housekeeper is a maintenance and analysis integration for Home Assistant. It creates a clear inventory of your installation, explains suspicious or orphaned objects, and shows how entities, devices, integrations, areas, and automations depend on each other.

The goal is not aggressive automatic cleanup. Housekeeper helps you understand what exists, why something is considered problematic, and what a cleanup or repair would affect before you confirm it.

> Housekeeper reads and analyzes first. It changes something only after you explicitly confirm a plan. Plans cover quarantine and removal, repairs, replacing references, renaming entities, assigning areas, deleting unused automations, trimming recorder history and other maintenance tasks. Depending on the action, Housekeeper requires a quarantine period, an additional confirmation and a successful backup. Reversible changes can be undone while their targets remain unchanged; irreversible recorder and backup deletions are clearly marked. Integrations and hubs are never modified, and Housekeeper changes only what a confirmed plan names.

## Screenshots

<p align="center">
  <img src="screenshots/showcase-en/overview-desktop-light.png" alt="Housekeeping overview" width="100%">
</p>

| Findings | Repair |
| --- | --- |
| ![Findings](screenshots/showcase-en/findings-desktop-light.png) | ![Repair](screenshots/showcase-en/repair-desktop-light.png) |

| Tidy up | Dependency path |
| --- | --- |
| ![Tidy up](screenshots/showcase-en/cleanup-desktop-light.png) | ![Dependency path](screenshots/showcase-en/graph-desktop-light.png) |

| Automations | Reliability |
| --- | --- |
| ![Automations](screenshots/showcase-en/runs-desktop-light.png) | ![Reliability](screenshots/showcase-en/reliability-desktop-light.png) |

## Why HA Housekeeper?

Mature Home Assistant installations often accumulate registry entries, unavailable entities, replaced devices, old statistics, and automation references that are difficult to assess safely. A missing state alone does not explain whether an entity was intentionally disabled, whether its integration is disabled, or whether the underlying device no longer exists.

Housekeeper combines registry data and the live Home Assistant runtime to provide that context in one administrator-only panel.

## Highlights

- **Inventory and diagnostics**: entities, devices, integrations, areas and automations in one place; every object is classified (active, unavailable, disabled, orphaned) with a reason.
- **Findings with impact**: broken references, orphaned and long-unavailable entities, possible duplicates, unused automations and low batteries, ranked by how much depends on them.
- **Dependencies**: see what an entity, device or automation is connected to, and what would break if you removed it.
- **Guided cleanup**: preview, explicit confirmation, backup, verification and undo, step by step. Nothing runs on its own.
- **Maintenance views**: batteries, reliability of integrations, recorder load and database, backup protection, automation runs and more.
- **Home functions**: put together important functions of your home (heating, alarm, photovoltaics) from your own objects and keep an eye on them, with history, availability and sensors. A mark such as “Offline on purpose” can apply only at night or at fixed times.
- **Exception rules and vacation mode**: leave out objects by area, label, integration or type, or only while a vacation entity or calendar says you are away, so that expected outages stay quiet.
- **AI access**: programs and AI agents that can call Home Assistant services (for example ha-mcp) read the findings and, if you allow it, mark them in Housekeeper's own list, never in Home Assistant. Off by default, with limits, an automatic switch-off, a log of every call and an undo.
- **Changes since the last scan**, sensors, repair hints, a scan button and the service `ha_housekeeper.scan` for your own dashboards and automations and a watch after updates: what stopped working after an update or restart.

## Quick start

1. Open HA Housekeeper in HACS with the button below, download it and restart Home Assistant.

   [![Open the HACS repository in My Home Assistant](https://my.home-assistant.io/badges/hacs_repository.svg)](https://my.home-assistant.io/redirect/hacs_repository/?owner=bertel2020&repository=HA-Housekeeper&category=integration)

2. **Add the integration** (not optional): **Settings → Devices & services → Add integration → HA Housekeeper**, or use the button below. Without this step no sidebar entry appears.

   [![Add HA Housekeeper to My Home Assistant](https://my.home-assistant.io/badges/config_flow_start.svg)](https://my.home-assistant.io/redirect/config_flow_start/?domain=ha_housekeeper)

3. Open **Housekeeper** in the sidebar as an administrator. The first scan runs automatically; **Scan now** refreshes it.
4. Start with **Findings** and open a finding to see the cause and what depends on it. Under **Clean up** you build a plan, which only shows a preview until you confirm it.

> New installs start in protection mode **read only**. To let Housekeeper change something, raise it under **Settings → Protection mode**.

More on installation (manual, custom repository), every view and all settings is in the **[User Guide](docs/USER-GUIDE.md)**.

## Safety in short

- The panel is for administrators only.
- Housekeeper reads and analyzes first; every change is a plan you confirm, with a backup where the action needs one.
- Integrations and hubs are never modified, no `.storage` file is edited directly, and nothing is cleaned up automatically.

Details: [Safety model](docs/USER-GUIDE.md#safety-model) and [Current limitations](docs/USER-GUIDE.md#current-limitations).

## Changelog

See [CHANGELOG.md](CHANGELOG.md) for release notes in English and German.

## Thanks to the contributors

Many thanks to [@jayjojayson](https://github.com/jayjojayson) for the contributions and feedback that helped improve HA Housekeeper.

## Disclaimer

HA Housekeeper is a privately developed, free open-source project and is provided
without warranty or guarantee. Use is at your own risk; in particular, no guarantee
can be given for error-free operation or for the correctness, completeness,
availability or lasting preservation of configuration and data. **Housekeeper can
change or remove entries, files and statistics in your Home Assistant installation.
Therefore make a Home Assistant backup before every cleanup and make independent
backups regularly, also outside the Home Assistant system.**

## License

This project is released under the [MIT License](LICENSE).
Copyright 2026 Roberto / bertel2020.

---

<a id="deutsch"></a>
<p align="center">
  <img src="https://raw.githubusercontent.com/bertel2020/HA-Housekeeper/main/custom_components/ha_housekeeper/brand/logo.png" alt="HA Housekeeper" width="160">
</p>

<h1 align="center">HA Housekeeper</h1>

<p align="center">
  Wartung und Analyse für Home Assistant: Inventar, Diagnose und Abhängigkeiten auf einen Blick.
</p>

<p align="center">
  <a href="https://github.com/hacs/integration"><img src="https://img.shields.io/badge/HACS-Custom-41BDF5.svg" alt="HACS Custom"></a>
  <a href="https://www.home-assistant.io/"><img src="https://img.shields.io/badge/Home%20Assistant-Custom%20Integration-18BCF2.svg?logo=home-assistant&logoColor=white" alt="Home Assistant"></a>
  <a href="https://github.com/bertel2020/HA-Housekeeper/releases"><img src="https://img.shields.io/github/v/release/bertel2020/HA-Housekeeper?sort=semver&include_prereleases" alt="Release"></a>
  <a href="https://github.com/bertel2020/HA-Housekeeper/actions/workflows/validate.yml"><img src="https://github.com/bertel2020/HA-Housekeeper/actions/workflows/validate.yml/badge.svg" alt="Validate"></a>
  <a href="LICENSE"><img src="https://img.shields.io/github/license/bertel2020/HA-Housekeeper" alt="License"></a>
</p>

<p align="center">
  <a href="https://buymeacoffee.com/bertel2020"><img src="https://img.shields.io/badge/Buy%20Me%20a%20Coffee-support-FFDD00?logo=buy-me-a-coffee&logoColor=black" alt="Buy Me a Coffee"></a>
  <a href="https://ko-fi.com/bertel2020"><img src="https://img.shields.io/badge/Ko--fi-support-FF5E5B?logo=ko-fi&logoColor=white" alt="Ko-fi"></a>
  <a href="https://paypal.me/RobertoMartins"><img src="https://img.shields.io/badge/PayPal-donate-00457C?logo=paypal&logoColor=white" alt="PayPal"></a>
</p>

HA Housekeeper ist eine Wartungs- und Analyseintegration für Home Assistant. Sie erstellt ein übersichtliches Inventar der Installation, erklärt verdächtige oder verwaiste Objekte und zeigt, wie Entitäten, Geräte, Integrationen, Bereiche und Automationen voneinander abhängen.

Das Ziel ist keine aggressive automatische Bereinigung. Housekeeper hilft zunächst zu verstehen, welche Objekte existieren, weshalb etwas als problematisch gilt und was eine Bereinigung oder Reparatur betreffen würde, bevor du sie bestätigst.

> Housekeeper liest und analysiert zunächst. Änderungen gibt es ausschließlich nach ausdrücklicher Bestätigung eines Plans. Pläne umfassen Quarantäne und Entfernen, Reparaturen, das Ersetzen von Verweisen, das Umbenennen von Entitäten, das Zuweisen von Bereichen, das Löschen ungenutzter Automationen, das Kürzen des Recorder-Verlaufs und weitere Wartungsaufgaben. Je nach Aktion verlangt Housekeeper eine Quarantänezeit, eine zusätzliche Bestätigung und ein erfolgreiches Backup. Umkehrbare Änderungen lassen sich zurücksetzen, solange ihre Ziele unverändert sind; endgültige Recorder- und Backup-Löschungen werden deutlich gekennzeichnet. Integrationen und Hubs werden nie verändert, und Housekeeper ändert nur, was ein bestätigter Plan nennt.

## Einblicke

<p align="center">
  <img src="screenshots/showcase/overview-desktop-light.png" alt="Housekeeping-Übersicht" width="100%">
</p>

| Befunde | Reparieren |
| --- | --- |
| ![Befunde](screenshots/showcase/findings-desktop-light.png) | ![Reparieren](screenshots/showcase/repair-desktop-light.png) |

| Aufräumen | Abhängigkeitspfad |
| --- | --- |
| ![Aufräumen](screenshots/showcase/cleanup-desktop-light.png) | ![Abhängigkeitspfad](screenshots/showcase/graph-desktop-light.png) |

| Automationen | Zuverlässigkeit |
| --- | --- |
| ![Automationen](screenshots/showcase/runs-desktop-light.png) | ![Zuverlässigkeit](screenshots/showcase/reliability-desktop-light.png) |


## Warum HA Housekeeper?

In gewachsenen Home-Assistant-Installationen sammeln sich häufig Registry-Einträge, nicht verfügbare Entitäten, ausgetauschte Geräte, alte Statistiken und schwer nachvollziehbare Automationsreferenzen an. Ein fehlender Zustand allein erklärt nicht, ob eine Entität absichtlich deaktiviert wurde, ihre Integration deaktiviert ist oder das zugrunde liegende Gerät nicht mehr existiert.

Housekeeper verbindet Registry-Daten mit der laufenden Home-Assistant-Instanz und stellt diesen Zusammenhang in einem gemeinsamen, nur für Administratoren erreichbaren Panel dar.

## Highlights

- **Inventar und Diagnose**: Entitäten, Geräte, Integrationen, Bereiche und Automationen an einem Ort; jedes Objekt wird mit Begründung eingeordnet (aktiv, nicht verfügbar, deaktiviert, verwaist).
- **Befunde mit Auswirkung**: defekte Verweise, verwaiste und lange nicht verfügbare Entitäten, mögliche Duplikate, ungenutzte Automationen und schwache Batterien, geordnet danach, wie viel daran hängt.
- **Abhängigkeiten**: sehen, womit eine Entität, ein Gerät oder eine Automation zusammenhängt und was beim Entfernen kaputtginge.
- **Geführtes Aufräumen**: Vorschau, ausdrückliche Bestätigung, Backup, Prüfung und Rückgängig, Schritt für Schritt. Nichts läuft von allein.
- **Wartungsansichten**: Batterien, Zuverlässigkeit der Integrationen, Recorder-Last und Datenbank, Backup-Schutz, Automationsläufe und mehr.
- **Hausfunktionen**: wichtige Funktionen des Hauses (Heizung, Alarm, Photovoltaik) aus eigenen Objekten zusammenstellen und im Blick behalten, mit Verlauf, Verfügbarkeit und Sensoren. Ein Vermerk wie „Absichtlich offline“ gilt auf Wunsch nur nachts oder zu festen Zeiten.
- **Ausnahmeregeln und Urlaubsmodus**: nimm Objekte nach Bereich, Label, Integration oder Typ aus, oder nur solange eine Urlaubs-Entität oder ein Kalender Abwesenheit meldet, damit erwartete Ausfälle ruhig bleiben.
- **KI-Zugriff**: Programme und KI-Agenten, die Home-Assistant-Dienste aufrufen können (zum Beispiel ha-mcp), lesen die Befunde und markieren sie auf Wunsch in Housekeepers eigener Merkliste, nie in Home Assistant. Standardmäßig aus, mit Grenzen, automatischem Ausschalten, einem Protokoll jedes Aufrufs und Zurücknehmen.
- **Änderungen seit dem letzten Scan**, Sensoren, Reparaturhinweise, ein Scan-Knopf und der Dienst `ha_housekeeper.scan` für eigene Dashboards und Automationen sowie die Beobachtung nach Updates: was nach einem Update oder Neustart nicht mehr läuft.

## Schnellstart

1. HA Housekeeper über den Button in HACS öffnen, herunterladen und Home Assistant neu starten.

   [![HACS-Repository in My Home Assistant öffnen](https://my.home-assistant.io/badges/hacs_repository.svg)](https://my.home-assistant.io/redirect/hacs_repository/?owner=bertel2020&repository=HA-Housekeeper&category=integration)

2. **Integration hinzufügen** (nicht optional): **Einstellungen → Geräte & Dienste → Integration hinzufügen → HA Housekeeper** oder über den Button. Ohne diesen Schritt erscheint kein Menüpunkt.

   [![HA Housekeeper zu My Home Assistant hinzufügen](https://my.home-assistant.io/badges/config_flow_start.svg)](https://my.home-assistant.io/redirect/config_flow_start/?domain=ha_housekeeper)

3. Als Administrator **Housekeeper** in der Seitenleiste öffnen. Der erste Scan läuft automatisch; **Neu scannen** aktualisiert ihn.
4. Mit **Befunde** beginnen und einen Befund öffnen: Ursache und Abhängigkeiten stehen oben. Unter **Aufräumen** baust du einen Plan, der bis zu deiner Bestätigung nur eine Vorschau zeigt.

> Neue Installationen starten im Schutzmodus **nur lesen**. Damit Housekeeper etwas ändern darf, erhöhe ihn unter **Einstellungen → Schutzmodus**.

Mehr zur Installation (manuell, eigenes Repository), zu allen Ansichten und Einstellungen steht im **[Benutzerhandbuch](docs/USER-GUIDE.de.md)**.

## Sicherheit in Kürze

- Das Panel ist nur für Administratoren.
- Housekeeper liest und analysiert zuerst; jede Änderung ist ein von dir bestätigter Plan, mit Backup, wo die Aktion eines braucht.
- Integrationen und Hubs werden nie verändert, keine `.storage`-Datei wird direkt bearbeitet, und nichts wird automatisch bereinigt.

Details: [Sicherheitsmodell](docs/USER-GUIDE.de.md#sicherheitsmodell) und [Aktuelle Einschränkungen](docs/USER-GUIDE.de.md#aktuelle-einschränkungen).

## Änderungsprotokoll

Die Versionshinweise auf Deutsch und Englisch stehen in [CHANGELOG.md](CHANGELOG.md).

## Dank an die Contributors

Vielen Dank an [@jayjojayson](https://github.com/jayjojayson) für die Beiträge und das Feedback, die HA Housekeeper besser gemacht haben.

## Haftungsausschluss

HA Housekeeper ist ein privat entwickeltes, kostenloses Open-Source-Projekt und wird
ohne Gewährleistung oder Garantie bereitgestellt. Die Nutzung erfolgt auf eigene
Verantwortung; insbesondere kann keine Garantie für einen fehlerfreien Betrieb sowie
für die Richtigkeit, Vollständigkeit, Verfügbarkeit oder den dauerhaften Erhalt von
Konfiguration und Daten übernommen werden. **Housekeeper kann Einträge, Dateien und
Statistiken in deiner Home-Assistant-Installation ändern oder entfernen. Lege daher
vor jedem Aufräumen ein Home-Assistant-Backup an und erstelle regelmäßig unabhängige
Backups, auch außerhalb des Home-Assistant-Systems.**

## Lizenz

Dieses Projekt steht unter der [MIT-Lizenz](LICENSE).
Copyright 2026 Roberto / bertel2020.
