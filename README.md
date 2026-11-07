# Legends Client

A custom launcher and in-game performance client for **Minecraft: Java Edition**, with a deep navy-blue interface and a focus on low resource usage.

> **Status: early development.** The launcher UI and Microsoft sign-in are implemented; game download and the in-game mod menu are in progress.
>
> Legends Client is **not an official Minecraft product** and is **not affiliated with, approved by, or associated with Mojang Studios or Microsoft.** You need a legitimate Minecraft: Java Edition license to play.

## Features

**Launcher (working / in progress)**
- Lightweight desktop app built with Tauri (uses the system WebView instead of bundling a browser).
- Sidebar navigation: Home, Versions, Cosmetics/Accounts, Settings.
- Microsoft account sign-in using the OAuth 2.0 device code flow.
- Account storage with refresh tokens kept in the operating system's secure credential store.
- Managed Java runtime (Azul Zulu) downloaded and verified with SHA-256.
- JVM profiles (balanced, max performance, low memory) with configurable RAM.
- Downloading game files directly from Mojang's servers *(in progress)*.

**In-game client (planned / prototype)**
- Fabric + Mixin based mod.
- Movable HUD modules: FPS, CPS, Keystrokes.
- Zoom and Fullbright.
- Mod menu to toggle modules and edit HUD positions.

## Tech stack

| Part | Technology |
|---|---|
| Launcher UI | React, TypeScript, Vite, TailwindCSS |
| Launcher backend | Rust, Tauri 2 |
| In-game client | Java, Fabric, Mixin |

## Authentication and privacy

Legends Client signs players in with their own Microsoft account:

1. Microsoft OAuth 2.0 device code flow (scopes: `XboxLive.signin offline_access`).
2. Xbox Live and XSTS token exchange.
3. Minecraft Services (`login_with_xbox`) and profile lookup to confirm the account owns Minecraft: Java Edition.

What the app does with your data:
- Refresh tokens are stored only in your operating system's credential store (Windows Credential Manager, macOS Keychain or Secret Service).
- Tokens are sent only to Microsoft, Xbox and Minecraft Services. They are never sent to any server operated by this project.
- The app does not collect analytics or personal data.
- Game files are downloaded from Mojang's official servers. Minecraft assets are not redistributed, and ownership checks are not bypassed.

## Building from source

Requirements: [Node.js](https://nodejs.org), [Rust](https://rustup.rs), and the [Tauri 2 prerequisites](https://v2.tauri.app/start/prerequisites/) for your OS.

```bash
git clone https://github.com/<your-user>/legends-client.git
cd legends-client
npm install
```

Sign-in needs your own Azure app registration (public client, personal Microsoft accounts) and its Application (client) ID:

```powershell
# Windows (PowerShell)
$env:LEGENDS_MS_CLIENT_ID="<your-client-id>"
npm run tauri dev
```

```bash
# macOS / Linux
LEGENDS_MS_CLIENT_ID="<your-client-id>" npm run tauri dev
```

Note: Minecraft Services only accepts apps approved by Mojang, so sign-in with a new client ID returns HTTP 403 until the app has been reviewed.

## Project structure

```
src/             React UI (launcher)
src-tauri/src/   Rust backend: accounts, Java runtime, game launch
client-mod/      In-game client (Fabric + Mixin)
```

## Roadmap

- [x] Launcher interface
- [x] Microsoft sign-in
- [x] Java runtime management and JVM profiles
- [ ] Minecraft version download from Mojang
- [ ] In-game mod menu and HUD editor
- [ ] Installers for Windows, macOS and Linux

## Contact

Questions or concerns about the app's use of Microsoft or Minecraft APIs: open an issue in this repository.

## License

To be defined. All rights reserved until a license is added.
