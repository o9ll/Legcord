# Building Legcord (o9ll fork)

This guide covers dependencies and build commands for **Windows 11**. The same Node/pnpm workflow also works on Linux and macOS.

## Dependencies

### Required

| Tool | Version | Notes |
| --- | --- | --- |
| [Node.js](https://nodejs.org/) | `>= 22` | Required by `package.json` (`engines.node`) |
| [pnpm](https://pnpm.io/) | `10.11.0` | Preferred package manager for this repo |
| [Git](https://git-scm.com/) | latest | Clone and version the source |

Install pnpm if needed:

```pwsh
npm install -g pnpm@10.11.0
```

### Recommended on Windows 11

| Tool | Purpose |
| --- | --- |
| [Visual Studio Build Tools](https://visualstudio.microsoft.com/visual-cpp-build-tools/) | Native modules (optional deps such as `@vencord/venmic`) |
| [Windows 11 SDK](https://developer.microsoft.com/windows/downloads/windows-sdk/) | Needed for AppX / Microsoft Store packaging |

### Project install

From the repository root:

```pwsh
git clone https://github.com/o9ll/Legcord.git
cd Legcord
pnpm install
```

`pnpm install` runs `electron-builder install-app-deps` automatically via `postinstall`.

## Windows 11 commands

### Run from source (development)

```pwsh
pnpm start
```

This runs `pnpm build` and launches Electron.

Build only, without launching:

```pwsh
pnpm build
```

### Package for Windows 11 (x64 installer + zip)

```pwsh
pnpm run package:win
```

Output goes to `dist/`:

- `Legcord-<version>-win-x64.exe` (NSIS installer)
- `Legcord-<version>-win-x64.zip` (portable archive)

### Unpacked build (fast local testing)

```pwsh
pnpm run package:win:dir
```

Creates an unpacked app in `dist/win-unpacked/` without producing an installer.

### All Windows targets (CI-style)

Builds x64, arm64, ia32, NSIS, AppX, and zip:

```pwsh
pnpm run package:win:all
```

### Lint before packaging

```pwsh
pnpm lint
pnpm build
```

## Portable mode on Windows

Place a folder named `legcord-data` next to the executable and start Legcord. Use the `.zip` build for portable installs.

## Releases

Prebuilt Windows packages are published on the fork's [GitHub Releases](https://github.com/o9ll/Legcord/releases) page.

## Upstream

This fork is based on [Legcord/Legcord](https://github.com/Legcord/Legcord).
