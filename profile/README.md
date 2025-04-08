# 🧑‍💻 Team-README: Projektübersicht & Zusammenarbeit

## 📦 Projektinfos

- **Technologie-Stack:** Laravel 11, Livewire 3.5, Jetstream, Spatie Permissions
- **Frontend:** Vite, Bootstrap 5, diverse JS-Plugins (z. B. DataTables, Chart.js, Toastr)
- **PHP-Version:** ^8.2
- **Testing:** PHPUnit, Laravel Pint für Code Style
- **Deployment-Ziel:** internes Intranet (kein Internet-Zugang im Zielsystem)
- **Template:** [NiceAdmin](https://bootstrapmade.com/demo/NiceAdmin/) von BootstrapMade

## ⚖️ Lokale Einrichtung

1. **Projekt klonen:**
   ```bash
   git clone git@github.com:dein-nutzername/dein-repo.git
   cd dein-repo
   ```
2. **Abhängigkeiten installieren:**
   ```bash
   composer install
   npm install
   ```
3. **Umgebung vorbereiten:**

   ```bash
   cp .env.example .env
   php artisan key:generate
   php artisan migrate --seed
   npm run dev
   ```

4. **Entwicklung starten:**
   ```bash
   composer dev
   ```
   _(Startet: Laravel Server, Queue Listener, Live-Log via Pail, Vite-Dev-Server)_

## 🛍️ Git-Workflow

### Branch-Konventionen

- `main`: Produktionsstand
- `develop`: Aktueller Entwicklungsstand
- `feature/*`: Neue Features
- `fix/*`: Bugfixes
- `refactor/*`: Umbauten am Code ohne neue Features

### Arbeiten im Team

1. Arbeite **immer in einem eigenen Branch**.
2. **Mache einen Pull Request (PR)** in `develop`.
3. Ein anderer Entwickler **reviewt und merged** den PR.

### Beispiel-Branch-Namen

- `feature/login-mit-2fa`
- `fix/datumsauswahl-im-modal`
- `refactor/user-service-cleanup`

## 📏 Code Style & Qualität

- Wir verwenden **Laravel Pint** für einheitliches Codeformat:
  ```bash
  ./vendor/bin/pint
  ```
- Tests lokal ausführen:
  ```bash
  php artisan test
  ```
- Git Pre-Commit Hook empfohlen (optional):
  ```bash
  # .git/hooks/pre-commit (ausführbar machen mit chmod +x)
  ./vendor/bin/pint
  php artisan test || exit 1
  ```

## 🧠 Absprachen

- **Keine Commits direkt in `main` oder `develop`**
- **Commit Messages klar und beschreibend:**
    - Gut: `fix: falsche Validierung bei E-Mail-Feld`
    - Schlecht: `Update Controller`
- **Regelmäßige Syncs bei größeren Änderungen** (z. B. Livewire-Komponenten, Migrations)

## 🗒️ Dokumentation

- Technische Notizen, Vorgehensweisen oder offene Fragen bitte in `docs/` als `.md` ablegen.
- Strukturvorschlag:
    - `docs/datenmodell.md`
    - `docs/rollen-und-berechtigungen.md`
    - `docs/deployment-intranet.md`

## 🚀 Deployment

- Das Projekt wird **nicht öffentlich deployed**, sondern im **Intranet ohne Internetzugang** betrieben.
- Geplantes Deployment via **Git Pull & Artisan Commands** auf internen Servern.
- Eventuell in Zukunft: interne CI/CD mit Jenkins, GitLab oder Ansible.

## 📆 Frontend-Struktur: NiceAdmin

- **Pfadstruktur:** Die meisten Admin-Vorlagen befinden sich unter `resources/views/layouts/`, `partials/`, `pages/`
- **Assets:** liegen unter `public/assets/` oder werden via Vite eingebunden (empfohlen: Assets modernisieren bei
  Bedarf)
- **Integration mit Blade & Livewire:**
    - UI-Elemente schrittweise in Blade-Komponenten auslagern (`resources/views/components/...`)
    - Livewire-Komponenten übernehmen die Logik (z. B. Tabellen, Formulare, Filter)
    - JS-Plugins mit `@push('scripts')` und `@stack('scripts')` einbinden
- **Vorsicht mit jQuery-basierten Plugins:** Bei Konflikten mit Livewire dominiert meist das Plugin – ggf. `wire:ignore`
  einsetzen
- **Layout-Anpassung:** zentrales Template unter `resources/views/layouts/app.blade.php`

## ✅ Nützliche Befehle (Kurzfassung)

```bash
composer dev          # Startet Server, Queue, Logs, Vite gleichzeitig
php artisan test      # Führt alle Tests aus
./vendor/bin/pint     # Formatiert den Code automatisch
npm run build         # Vite-Build für Produktion
```

# Branch-Regelset: `main`

- **Ziel:** Branch
- **Quelle:** Repository `Reg-Ex-co/conncert`
- **Durchsetzung:** Aktiv
- **Gilt für:** Standard-Branch (`~DEFAULT_BRANCH`)

---

## 🛡️ Regeln

### 1. 🔒 Löschen verhindern

> Das Löschen des Branches ist nicht erlaubt.

### 2. ⛔ Keine Non-Fast-Forward-Pushes

> Nur Fast-Forward-Pushes sind erlaubt – Rewrites der Branch-Historie sind untersagt.

### 3. 🧬 Lineare Historie erforderlich

> Die Commit-Historie muss linear bleiben, d. h. keine Merge-Commits außerhalb von Pull Requests.

### 4. 🔍 Pull-Request-Anforderungen

- ✅ **Mindestens eine genehmigende Review** erforderlich
- 🔄 **Reviews werden verworfen**, wenn nachträglich Commits gepusht werden
- 🟡 **Letzter Push muss nicht erneut genehmigt werden**
- 💬 **Offene Review-Threads müssen nicht aufgelöst sein**
- 🤖 **Automatische Copilot-Code-Reviews sind deaktiviert**

#### ✅ Erlaubte Merge-Methoden:

- **Merge** – klassisches Zusammenführen
- **Squash** – Commits zusammenfassen
- **Rebase** – Commits neu aufsetzen

---

## 🚨 Ausnahmen (Bypass)

- Benutzer mit der **Rolle `RepositoryRole`** (ID: `5`) dürfen die Regeln **immer umgehen**.

---

Bei Fragen: lieber **frühzeitig nachfragen als spät flicken** 😉

Happy Coding! 💻
