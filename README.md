# SOBST Warfare Systems

Space Engineers Workshop mod repository for SOBST Warfare Systems.

This repository follows the same project shape as `PressurizerProjects`: root MSBuild props/targets provide Space Engineers binary references, each Workshop item has its own project folder, and projects target .NET Framework 4.8 with MDK2 analyzers.

## Layout

- `SOBST-Warfare-Systems.sln` - solution file.
- `SOBSTWarfareSystemsWC/SOBSTWarfareSystemsWC.csproj` - WeaponCore edition project.
- `SOBSTWarfareSystemsNonWC/SOBSTWarfareSystemsNonWC.csproj` - non-WeaponCore edition project.
- `SOBSTWarfareSystemsWC/src` - Workshop `2854025571` payload.
- `SOBSTWarfareSystemsNonWC/src` - Workshop `2813510420` payload.
- `Directory.Build.props` - resolves `SpaceEngineersDir` from `SE_DIR`, `SE_GAME_ROOT`, or local user props, and optionally resolves `WeaponCoreDir` from `WEAPONCORE_DIR`.
- `Directory.Build.targets` - adds Space Engineers binary references and optional WeaponCore references when present.
- `.github/workflows/steam-workshop-upload-wc.yml` - uploads the WeaponCore Workshop payload from pushes to `production`.
- `.github/workflows/steam-workshop-upload-non-wc.yml` - uploads the non-WeaponCore Workshop payload from pushes to `production`.

## Local Setup

Set the Space Engineers path with one of:

```bash
export SE_DIR="/path/to/steamapps/common/SpaceEngineers"
```

or copy `Directory.Build.user.props.example` to `Directory.Build.user.props` and edit the path.

If you have local WeaponCore reference binaries, set:

```bash
export WEAPONCORE_DIR="/path/to/WeaponCore"
```

MDK2 also reads a project-local binary path file. Copy the examples if these files do not already exist:

```bash
cp SOBSTWarfareSystemsWC/SOBSTWarfareSystemsWC.mdk.local.ini.example SOBSTWarfareSystemsWC/SOBSTWarfareSystemsWC.mdk.local.ini
cp SOBSTWarfareSystemsNonWC/SOBSTWarfareSystemsNonWC.mdk.local.ini.example SOBSTWarfareSystemsNonWC/SOBSTWarfareSystemsNonWC.mdk.local.ini
```

Build:

```bash
dotnet restore
dotnet build
```

## Workshop Uploads

The GitHub Actions workflows upload to Steam Workshop on pushes to `production`.

- Changes under `SOBSTWarfareSystemsWC/src/**` run the WC workflow and upload Workshop item `2854025571`.
- Changes under `SOBSTWarfareSystemsNonWC/src/**` run the non-WC workflow and upload Workshop item `2813510420`.

Required repository secrets for the WC item:

- `SOBST_WC_STEAM_USERNAME`
- `SOBST_WC_STEAM_CONFIG_VDF`

Required repository secrets for the non-WC item:

- `SOBST_NON_WC_STEAM_USERNAME`
- `SOBST_NON_WC_STEAM_CONFIG_VDF`
