# MachineHealth releases

Signed builds of MachineHealth, a monitor for a Windows or Linux machine: tray status,
alerts, history and a local dashboard. The source code is private; this repository holds
only releases.

Each release has:

- `MachineHealth.exe`: the Windows app, one file.
- `machinehealth-linux-x86_64`: the Linux app.
- `manifest.json` and `manifest.json.sig`: the version and each file's SHA-256 and size,
  signed with the release key.
- A zip and a tar.gz for a manual install, each with a `.sha256`.

An installed MachineHealth updates itself from here. Before it replaces anything, it checks
that `manifest.json` is signed by the release key compiled into it, that the version is
newer, and that the downloaded file's SHA-256 and size match the manifest. A file that is
not from a signed release is never installed.
