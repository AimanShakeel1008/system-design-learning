# Troubleshooting

Decodes the errors the labs are likely to throw, in plain language. Grows as labs grow.

## Setup (Lesson 00)

### `winget` is not recognized
Windows can't find the package manager. It ships via the "App Installer" app — open the Microsoft Store, search **App Installer**, update/install it, then open a new terminal.

### I installed a tool but the terminal says it is not recognized
The shell reads its list of program folders (the PATH) once, at terminal startup, so a terminal opened *before* the install can't see the new tool. Close the terminal, open a new one, try again.

### `docker: error during connect: ... the system cannot find the file specified`
The `docker` command is only a messenger; the actual engine runs inside the Docker Desktop app, and it isn't running. Start **Docker Desktop** from the Start menu, wait for the whale icon / "running" status, retry.

### Docker Desktop install complains about WSL 2 or virtualization
Docker on Windows runs inside a lightweight Linux layer called WSL 2, which needs hardware virtualization switched on.
1. In PowerShell **as administrator**: `wsl --install`, then restart.
2. If it still complains, virtualization is disabled in the BIOS/UEFI: reboot into firmware settings and enable "Intel VT-x" / "AMD-V" / "SVM Mode" (the name varies by manufacturer).

### Typing `python` opens the Microsoft Store
Windows ships a fake `python` command that advertises the Store, and it shadows the real install. Fix: **Settings → Apps → Advanced app settings → App execution aliases**, switch **off** the `python.exe` and `python3.exe` entries. New terminal, retry `python --version`.

### `curl` behaves strangely in PowerShell (asks for a `-Uri`, weird table output)
PowerShell aliases `curl` to its own `Invoke-WebRequest`, a different tool. Always type `curl.exe` so the real curl runs.

### `git push` asks who I am or rejects authentication
GitHub no longer accepts plain passwords from the command line. On the first push, a browser window ("Git Credential Manager") should open — sign in to GitHub there and it is remembered. If the window never appears, run `git config --global credential.helper manager` and push again.
