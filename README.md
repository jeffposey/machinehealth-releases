# MachineHealth releases

MachineHealth watches your machine, works out what is wrong when something goes wrong, and
tells you what to do about it.

- **AI investigations and recommendations.** When a process runs away, memory climbs, or a
  reading leaves its normal range, one click starts an investigation. A Claude Code agent
  reads the evidence (the machine's own history, the processes involved, what changed
  recently) through read-only tools, then writes a report: what it found, how sure it is,
  and what it recommends, such as restarting a leaking program, ending a stuck process, or
  rebooting. Nothing happens until you approve it, and your verdict on each report is kept,
  so you can see how often it was right.
- **Knows the software on your machine.** Profiles for the programs you run, what is normal
  for each, and an optional automatic restart for a program you know leaks.
- **Where your memory actually went.** A breakdown of commit and RAM, including the memory
  no process owns, which Task Manager doesn't show.
- **Alerts worth acting on.** Tray icon colour, Windows notifications and phone push, with
  rules that catch a climb hours before it hits a limit and stay quiet otherwise.
- **History and a dashboard you can reach from your phone.** One-minute history with graphs
  of CPU, GPU, memory, disks and temperatures (NVMe health included), on a local dashboard
  you can open remotely from mobile devices through Tailscale. Plus a REST API.

Windows and Linux (headless). Investigations use Claude Code if it is installed.

## Install on Windows

Download [machinehealth-setup.exe](https://github.com/jeffposey/machinehealth-releases/releases/latest/download/machinehealth-setup.exe)
and run it. It is unsigned for now, so SmartScreen warns on the first run: More info, then
Run anyway. It asks for admin once, installs into `%LOCALAPPDATA%\Programs\MachineHealth`,
registers a sign-in task that starts it elevated, and starts it. It offers to install
PawnIO, the driver that lets it read CPU temperature. Run a newer setup to upgrade in place;
your data in `%USERPROFILE%\.machinehealth` is kept. Uninstall from Settings > Apps.

## Install on Linux

Headless: a systemd user unit, with the dashboard, the API and Web Push as the whole
interface. No sudo.

```sh
curl -LO https://github.com/jeffposey/machinehealth-releases/releases/latest/download/machinehealth-linux-x86_64
curl -LO https://github.com/jeffposey/machinehealth-releases/releases/latest/download/install-linux.sh
sh install-linux.sh
```

The script installs the binary beside it to `~/.local/bin/machinehealth`, writes
`~/.config/systemd/user/machinehealth.service`, and enables and starts it. The dashboard is
on `http://localhost:8890/app/`. It prints, and never runs, the two commands that need root:
`loginctl enable-linger` to start at boot rather than at login, and a udev rule for reading
NVMe health.

## What's in a release

| File | What it is |
| --- | --- |
| `machinehealth-setup.exe` | The Windows installer. |
| `MachineHealth.exe` | The Windows app, one file. Installed copies update to it. |
| `machinehealth-linux-x86_64` | The Linux app, one file. Installed copies update to it. |
| `install-linux.sh` | The Linux install: the binary beside it and the systemd user unit. |
| `manifest.json` | The version and the SHA-256 and size of the files above. |
| `manifest.json.sig` | The release key's signature of `manifest.json`. |

GitHub adds "Source code (zip)" and "Source code (tar.gz)" to every release and has no
setting to remove them. They hold only this README: ignore them.

## Updates

An installed MachineHealth updates itself from here. Before it replaces anything, it checks
that `manifest.json` is signed by the release key compiled into it, that the version is
newer, and that the downloaded file's SHA-256 and size match. Nothing that is not from a
signed release is ever installed. To check a download by hand, compare its SHA-256 with
`manifest.json`.

The source code is private; this repository holds only releases.
