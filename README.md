# NZBDrop – SABnzbd iOS/iPadOS Client

Modern SwiftUI frontend for SABnzbd servers.

## Projektstruktur

```
NZBDrop/
├── NZBDropApp.swift              App-Einstiegspunkt, Onboarding-Routing
├── ContentView.swift             TabView (iPhone) / NavigationSplitView (iPad)
│
├── Models/
│   ├── QueueItem.swift           SABnzbd Queue-Datenmodell (Decodable)
│   ├── HistoryItem.swift         History-Einträge
│   └── ServerStats.swift         Stats / Status Responses
│
├── Services/
│   ├── AppSettings.swift         @AppStorage-gesicherter Settings-Dienst
│   └── SABnzbdAPI.swift          Kompletter API-Client (async/await)
│
├── ViewModels/
│   ├── QueueViewModel.swift      Polling, Queue-Aktionen
│   ├── HistoryViewModel.swift    History + Pagination
│   └── StatsViewModel.swift      Stats & Status
│
├── Views/
│   ├── Queue/
│   │   ├── QueueView.swift       Downloads-Hauptscreen
│   │   ├── ServerStatusCard.swift Geschwindigkeit/ETA-Karte
│   │   └── QueueItemRow.swift    Einzelner Queue-Eintrag
│   ├── History/
│   │   ├── HistoryView.swift     History-Screen mit Filter-Chips
│   │   └── HistoryItemRow.swift  Einzelner History-Eintrag
│   ├── Stats/
│   │   └── StatsView.swift       KPI-Kacheln, Disk, Server-Info
│   ├── Settings/
│   │   ├── SettingsView.swift    Form mit Connection-Test
│   │   └── ServerProfileCard.swift Profile-Karte oben
│   └── Onboarding/
│       └── OnboardingView.swift  Erster-Start-Wizard
│
└── Utilities/
    └── Extensions.swift          Color, Date, View-Helfer
```

## Setup in Xcode

1. **Neues Projekt erstellen:**
   - File → New → Project → iOS → App
   - Product Name: `NZBDrop`
   - Interface: **SwiftUI**
   - Language: **Swift**
   - Minimum Deployment: **iOS 17.0**

2. **Alle Dateien hinzufügen:**
   - Vorhandene `ContentView.swift` löschen
   - Alle Swift-Dateien aus diesem Gerüst per Drag & Drop in Xcode ziehen
   - „Copy items if needed" aktivieren
   - Gruppenstruktur beibehalten (Create Groups)

3. **AccentColor setzen:**
   - In `Assets.xcassets` → `AccentColor` → auf `#4F8EF7` setzen

4. **App-Icon:**
   - Platzhalter in `Assets.xcassets` → `AppIcon` ersetzen

5. **Capabilities (optional):**
   - Für Push-Notifications: Signing & Capabilities → + Push Notifications

6. **Starten:**
   - Simulator oder echtes Gerät wählen → ▶ Run

## Unterstützte SABnzbd API Endpoints

| Feature            | API-Aufruf                         |
|--------------------|------------------------------------|
| Queue laden        | `?mode=queue`                      |
| Queue pausieren    | `?mode=pause` / `?mode=resume`     |
| Job pausieren      | `?mode=queue&name=pause&value=ID`  |
| Job löschen        | `?mode=queue&name=delete&value=ID` |
| Priorität setzen   | `?mode=queue&name=priority`        |
| History laden      | `?mode=history`                    |
| History löschen    | `?mode=history&name=delete`        |
| Retry (fehlgeschl.)| `?mode=retry`                      |
| Server-Status      | `?mode=status`                     |
| Verbindungstest    | `?mode=version`                    |
| Speed-Limit        | `?mode=config&name=speedlimit`     |

## Mindestanforderungen

- iOS / iPadOS 17.0+
- Xcode 15.0+
- SABnzbd 3.x oder 4.x
