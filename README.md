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

Windows and Linux (headless). One file, no admin needed to run; a few sensors (CPU
temperature) need it and say so. Investigations use Claude Code if it is installed.

## What's in a release

- `MachineHealth.exe`: the Windows app, one file.
- `machinehealth-linux-x86_64`: the Linux app.
- `manifest.json` and `manifest.json.sig`: the version and each file's SHA-256 and size,
  signed with the release key.
- A zip and a tar.gz for a manual install, each with a `.sha256`.

## Updates

An installed MachineHealth updates itself from here. Before it replaces anything, it checks
that `manifest.json` is signed by the release key compiled into it, that the version is
newer, and that the downloaded file's SHA-256 and size match. Nothing that is not from a
signed release is ever installed.

The source code is private; this repository holds only releases.
