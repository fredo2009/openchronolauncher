# OpenChrono Launcher

Mini-navigateur dédié (basé sur WebView2 / Chromium) qui charge
`https://openchrono.fr/transfert` **sans les sécurités CORS / mixed content**,
pour que la page puisse dialoguer avec le logiciel de chrono en HTTP local/VPN.

L'exe n'embarque que l'URL : toute modif de la page côté serveur est prise en
compte au rechargement (touche **F5**).

---

## Prérequis (machine de dev)

- [.NET SDK 8](https://dotnet.microsoft.com/download) installé.

## Compiler le .exe unique

Dans le dossier du projet :

```bash
dotnet publish -c Release
```

L'exécutable se trouve ici :

```
bin/Release/net8.0-windows/win-x64/publish/OpenChronoLauncher.exe
```

C'est un seul fichier portable (le runtime .NET est embarqué).

## Prérequis (machine cible / poste de chrono)

- **WebView2 Runtime** doit être présent.
  - Déjà préinstallé sur Windows 11 et la plupart des Windows 10 à jour.
  - Sinon, installer le « Evergreen Bootstrapper » (~2 Mo) :
    https://developer.microsoft.com/microsoft-edge/webview2/

---

## Personnalisation

- **Ajouter / modifier un onglet** : tableau `Tabs` en haut de `Program.cs`.
  Une ligne = un onglet, au format `("Titre", "https://...")`.
- **Mode plein écran / kiosque** : remplacer dans `MainForm()` par
  `FormBorderStyle = FormBorderStyle.None;` + `WindowState = FormWindowState.Maximized;`.
- **Icône** : ajouter `<ApplicationIcon>app.ico</ApplicationIcon>` dans le .csproj.

## Raccourcis

- **F5** : recharger la page (récupère la dernière version serveur)
- **F12** : ouvrir les outils de développement (console réseau pour débugger)