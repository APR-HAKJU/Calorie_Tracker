# 📝 Git Cheatsheet - Grundlagen

Dieses Cheatsheet enthält die wichtigsten Git-Befehle für die tägliche Arbeit.

---

## 🔑 SSH-Key Setup (Einmalig)

### 1. SSH-Key generieren

```bash
ssh-keygen -t ed25519 -C "deine.email@example.com"
```

**Was passiert:**

- Du wirst nach einem Speicherort gefragt → **Enter drücken** (Standard-Pfad verwenden)
- Du wirst nach einem Passwort gefragt → **Enter drücken** (leer lassen) ODER sicheres Passwort eingeben
- Der SSH-Key wird erstellt

### 2. SSH-Key anzeigen

**Linux/Mac:**

```bash
cat ~/.ssh/id_ed25519.pub
```

**Windows:**

```bash
type %userprofile%\.ssh\id_ed25519.pub
```

**Oder alternativ:**

```bash
cat ~/.ssh/id_ed25519.pub
```

### 3. SSH-Key zu GitHub hinzufügen

1. Kopiere den kompletten SSH-Key (beginnt mit `ssh-ed25519`)
2. Gehe zu GitHub → **Settings** (oben rechts auf dein Profilbild klicken)
3. Links im Menü: **SSH and GPG keys**
4. Klicke auf **New SSH key**
5. **Title:** "Mein Laptop" (oder ein beliebiger Name)
6. **Key:** Füge den kopierten SSH-Key ein
7. Klicke auf **Add SSH key**

### 4. SSH-Verbindung testen

```bash
ssh -T git@github.com
```

**Erwartete Ausgabe:**

```
Hi DEIN-USERNAME! You've successfully authenticated, but GitHub does not provide shell access.
```

✅ **Perfekt! SSH ist eingerichtet.**

---

## 🚀 Git Grundbefehle (Ohne Branches)

### Repository clonen

```bash
git clone git@github.com:DEIN-USERNAME/REPO-NAME.git
```

**Beispiel:**

```bash
git clone git@github.com:max123/Kalorientracker.git
```

In das Projektverzeichnis wechseln:

```bash
cd Kalorientracker
```

---

## 📋 Der Standard-Workflow

### 1. Status prüfen

```bash
git status
```

**Was zeigt es:**

- Welche Dateien wurden geändert (rot = nicht staged)
- Welche Dateien sind zum Commit bereit (grün = staged)
- Auf welchem Branch du bist

**Tipp:** Verwende diesen Befehl häufig, um zu sehen was los ist!

---

### 2. Änderungen hinzufügen (Add)

**Alle geänderten Dateien hinzufügen:**

```bash
git add .
```

**Einzelne Datei hinzufügen:**

```bash
git add dateiname.py
```

**Mehrere Dateien hinzufügen:**

```bash
git add datei1.py datei2.py datei3.py
```

**Was macht `git add`?**

- Markiert Dateien für den nächsten Commit
- Die Dateien sind jetzt "staged" (bereit zum Committen)

---

### 3. Commit erstellen

```bash
git commit -m "Deine Commit-Nachricht hier"
```

**Beispiele für gute Commit-Nachrichten:**

```bash
git commit -m "User Model mit SQLAlchemy erstellt"
git commit -m "Login-Funktion implementiert"
git commit -m "Bug in Kalorienberechnung behoben"
git commit -m "README mit Installationsanleitung erweitert"
```

**Was macht `git commit`?**

- Speichert einen "Snapshot" deiner Änderungen
- Erstellt einen Eintrag in der Git-Historie
- Nur staged Dateien werden committed

---

### 4. Änderungen hochladen (Push)

```bash
git push
```

**Oder explizit:**

```bash
git push origin main
```

**Was macht `git push`?**

- Lädt deine lokalen Commits zu GitHub hoch
- Andere können deine Änderungen jetzt sehen
- `origin` = das Remote Repository auf GitHub
- `main` = der Branch-Name

---

### 5. Änderungen herunterladen (Pull)

```bash
git pull
```

**Oder explizit:**

```bash
git pull origin main
```

**Was macht `git pull`?**

- Lädt Änderungen von GitHub herunter
- Integriert sie in deine lokale Kopie
- Wichtig bevor du anfängst zu arbeiten!

---

## 🔄 Der komplette Workflow

So sieht ein typischer Arbeitsablauf aus:

```bash
# 1. Neueste Änderungen holen
git pull

# 2. Arbeiten: Dateien erstellen/bearbeiten
# ... Code schreiben ...

# 3. Status prüfen
git status

# 4. Änderungen hinzufügen
git add .

# 5. Commit erstellen
git commit -m "Feature XY implementiert"

# 6. Auf GitHub hochladen
git push
```

---

## 📊 Weitere nützliche Befehle

### Commit-Historie anzeigen

```bash
git log
```

**Kompakte Ansicht:**

```bash
git log --oneline
```

**Letzte 5 Commits:**

```bash
git log --oneline -5
```

### Änderungen anzeigen (vor dem Add)

```bash
git diff
```

**Was wurde in einer bestimmten Datei geändert:**

```bash
git diff dateiname.py
```

### Änderungen verwerfen (VORSICHT!)

**Einzelne Datei zurücksetzen:**

```bash
git checkout -- dateiname.py
```

**Alle Änderungen verwerfen:**

```bash
git checkout -- .
```

⚠️ **Achtung:** Diese Änderungen sind unwiderruflich verloren!

---

## 🆘 Häufige Probleme

### Problem: "Permission denied (publickey)"

**Lösung:** SSH-Key nicht richtig eingerichtet

```bash
# SSH-Key neu generieren
ssh-keygen -t ed25519 -C "deine.email@example.com"

# SSH-Key anzeigen und zu GitHub hinzufügen
cat ~/.ssh/id_ed25519.pub
```

### Problem: "fatal: not a git repository"

**Lösung:** Du bist nicht in einem Git-Projekt

```bash
# Prüfe ob du im richtigen Ordner bist
pwd

# Wechsle in den Projektordner
cd Kalorientracker
```

### Problem: "Your branch is behind"

**Lösung:** Andere haben Änderungen gepusht

```bash
git pull
```

### Problem: Commit-Nachricht falsch geschrieben

**Lösung:** Letzten Commit-Message ändern

```bash
git commit --amend -m "Neue bessere Nachricht"
```

⚠️ **Nur verwenden BEVOR du gepusht hast!**

### Problem: Datei vergessen hinzuzufügen

**Lösung:** Datei nachträglich zum letzten Commit hinzufügen

```bash
git add vergessene_datei.py
git commit --amend --no-edit
```

⚠️ **Nur verwenden BEVOR du gepusht hast!**

---

## 💡 Best Practices

### ✅ Do's

- **Häufig committen:** Nach jedem abgeschlossenen Task
- **Gute Commit-Messages:** Beschreibe was du gemacht hast
- **Vor Arbeitsbeginn pullen:** Hol dir die neuesten Änderungen
- **Nach Arbeit pushen:** Teile deine Änderungen mit dem Team

### ❌ Don'ts

- **Große Commits vermeiden:** Nicht 20 Änderungen auf einmal committen
- **Schlechte Messages:** "fix", "update", "changes" sagen nichts aus
- **Sensible Daten:** Passwörter, API-Keys NIEMALS committen
- **Große Binärdateien:** Videos, große Bilder nicht in Git

---

## 🎯 Schnellreferenz

| Befehl                | Beschreibung                |
| --------------------- | --------------------------- |
| `git status`          | Zeigt Status der Dateien    |
| `git add .`           | Fügt alle Änderungen hinzu  |
| `git add datei.py`    | Fügt eine Datei hinzu       |
| `git commit -m "..."` | Erstellt einen Commit       |
| `git push`            | Lädt Commits zu GitHub hoch |
| `git pull`            | Holt Änderungen von GitHub  |
| `git log --oneline`   | Zeigt Commit-Historie       |
| `git diff`            | Zeigt Änderungen an         |

---

## 🔗 Weiterführende Ressourcen

- [Git Cheat Sheet (PDF)](https://education.github.com/git-cheat-sheet-education.pdf)
- [Git Dokumentation](https://git-scm.com/doc)
- [GitHub Guides](https://guides.github.com/)

---

**Tipp:** Drucke dieses Cheatsheet aus oder speichere es als Lesezeichen! 📌
