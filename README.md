# scoop-bucket

[![Tests](https://github.com/wolffshots/scoop-bucket/actions/workflows/ci.yml/badge.svg)](https://github.com/wolffshots/scoop-bucket/actions/workflows/ci.yml) [![Excavator](https://github.com/wolffshots/scoop-bucket/actions/workflows/excavator.yml/badge.svg)](https://github.com/wolffshots/scoop-bucket/actions/workflows/excavator.yml)

A [Scoop](https://scoop.sh) bucket for [wolffshots](https://github.com/wolffshots)
tools on Windows. It is the Windows counterpart of
[homebrew-tap](https://github.com/wolffshots/homebrew-tap).

## patreon-posts

A terminal UI for browsing Patreon posts, with SQLite caching and YouTube link
extraction.

### Install

```powershell
scoop bucket add wolffshots https://github.com/wolffshots/scoop-bucket
scoop install wolffshots/patreon-posts
```

This installs the prebuilt release binary for x64 or ARM64. Go is not needed.

### Configuration

The config file is `%USERPROFILE%\.patreon-posts.json`. See the
[patreon-posts repository](https://github.com/wolffshots/patreon-posts#configuration)
for the settings and for reading cookies from a Firefox-family browser.

### Upgrade

```powershell
scoop update
scoop update patreon-posts
```

## fftui

A terminal UI for tracking Future Forex arbitrage cycle returns.

### Install

```powershell
scoop bucket add wolffshots https://github.com/wolffshots/scoop-bucket
scoop install wolffshots/fftui
```

This installs the prebuilt x64 release binary. fftui has no ARM64 Windows build.

### Configuration

Create the config file (`%AppData%\fftui\config.env`) with `fftui --init-config`,
then fill in your credentials. See the
[fftui repository](https://github.com/wolffshots/fftui#credentials) for every key.

### Upgrade

```powershell
scoop update
scoop update fftui
```

## How updates work

Unlike the Homebrew tap, nothing here is edited by hand on release. The
[Excavator](.github/workflows/excavator.yml) workflow runs every 4 hours. It
checks each app's latest GitHub release (`checkver`), rewrites the manifest's
version and URLs, reads the new hashes from the release's `checksums.txt`
(`autoupdate`), and commits the result. To pick up a release straight away, run
the Excavator workflow by hand from the Actions tab.

A manifest only works while its source repository is public, because Scoop
downloads release assets without logging in.

## Adding another app

1. The app's release must include a Windows `.exe` (or `.zip`) and a
   `checksums.txt` in `sha256sum` format.
2. Copy `bucket/patreon-posts.json` to `bucket/<app>.json` and change the names
   and URLs.
3. Push. Excavator fills in the version and hashes on its next run.

Check a manifest locally with `.\bin\checkver.ps1 <app>` and
`.\bin\checkurls.ps1 <app>` (these need Scoop installed).
