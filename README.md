# scoop-bucket

A [Scoop](https://scoop.sh) bucket with one app in it:
[PC GamePak](https://github.com/HarryBMa/pc-gamepak), which turns removable
storage into physical game cartridges.

```powershell
scoop bucket add harrybma https://github.com/HarryBMa/scoop-bucket
scoop install pc-gamepak
```

That puts `pc-gamepak` and `pc-gamepak-watcher` on your PATH. The wizard works
straight away:

```powershell
pc-gamepak --create
```

The watcher is what opens a launcher when a cartridge is plugged in, and Scoop
cannot register it to start at logon. Run the installer once to do that:

```powershell
powershell -ExecutionPolicy Bypass -File "$(scoop prefix pc-gamepak)\windows\install.ps1" -Mode Watcher
```

`-Mode Watcher` matters: without it the script asks which mode to install, and a
non-interactive shell cannot answer.

To undo it later:

```powershell
powershell -File "$(scoop prefix pc-gamepak)\windows\uninstall.ps1"
```

## Updating

The manifest carries `checkver` and `autoupdate`, so a new tagged release is
picked up by `scoop update` once the manifest here is bumped — either by hand or
with `bin/checkver.ps1 -u` from a Scoop checkout.

Issues with the app belong on
[the main repository](https://github.com/HarryBMa/pc-gamepak/issues); this one is
just the manifest.
