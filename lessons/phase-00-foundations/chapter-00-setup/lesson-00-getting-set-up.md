# Lesson 00 — Getting Set Up

**Phase 0 — How to Think About Systems · Chapter 00: Setup · Lesson 00**

- **Covers:** the course toolchain (Git + GitHub, Docker + Docker Compose, Python 3, curl, dig/nslookup, jq) and the course conventions (design docs, ASCII + Mermaid diagrams, the living toolkit)
- **Files created:** this lesson; seeds for `glossary.md`, `toolkit.md`, `README.md`, `troubleshooting.md`
- **Prerequisites:** none — this is the first lesson

---

## SECTION 1 — WHY THIS MATTERS

This course is built on a promise: you will not just read about systems, you will run them on your own machine and watch them behave. Databases, caches, message brokers, web servers, load tests — all of it runs locally, for free.

That promise needs tools. Without them:

- No **Git/GitHub** → no permanent history of your work and no public portfolio to show for it.
- No **Docker** → every lab would begin with an hour of painful manual installation, and your machine would slowly fill with half-configured software.
- No **Python** → no way to run the small experiments that make abstract ideas (latency gaps, hash rings, rate limiters) concrete.
- No **curl / dig / jq** → the machinery of the internet stays invisible, and you have to take my word for how it works. Taking someone's word for it is exactly what this course refuses to do.

Every tool installed today is used repeatedly later. Nothing here is ceremony.

---

## SECTION 2 — REAL WORLD ANALOGY

Setting up a workshop before learning carpentry.

| Workshop item | Our equivalent | What it's for |
|---|---|---|
| The workbench | The terminal | Where all work actually happens |
| The tool catalog you order from | winget (package manager) | Get any tool with one command |
| The project binder with every draft | Git repository | Every version of your work, forever |
| The fireproof safe off-site | GitHub | A copy that survives your laptop dying |
| Standard shipping crates | Docker containers | Any machinery arrives ready-to-run, leaves without a trace |
| The multi-crate delivery manifest | Docker Compose | Several crates arrive and start together |
| The sketchpad | Python | Quick experiments to test an idea |
| Magnifying glass, phone book, label maker | curl, dig, jq | Inspect the invisible up close |

A carpenter who skips workshop setup spends every project fighting their tools. Same here.

---

## SECTION 3 — THE CONCEPT EXPLAINED

### The terminal and the shell

A **terminal** is a program where you type text commands and read text answers. It survives from the pre-mouse era because it is faster, more precise, and scriptable — and because the servers you will design for have no screens or mice at all; they are administered entirely by typed commands. The program that interprets what you type is the **shell**. Windows 11's built-in shell is **PowerShell** (Windows key → type `powershell` → Enter).

### The package manager

Installing by download-and-click works but is slow, manual, and unrepeatable. A **package manager** installs software from a single typed command, like ordering by catalog number instead of browsing shelves. Windows ships with **winget**.

### Git, repositories, commits

**Version control** keeps every saved snapshot of a project with a note about what changed, and can restore any file to any earlier state. It exists because "final-v2-REALLY-final.doc" is how work gets lost. **Git** is the universal version-control tool.

- A **repository (repo)**: a folder tracked by Git — the files plus their entire history.
- A **commit**: one saved snapshot, with a message describing the change.
- **GitHub**: a website holding an online copy of your repo — backup plus portfolio.
- A **remote**: your repo's online copy, from the local repo's point of view.
- A **push**: sending your new commits up to the remote.
- **.gitignore**: a list of files Git must never record. Ours excludes the course's private control files and any real secrets — because Git history is permanent and gets copied to GitHub, a secret committed once is leaked forever.

### Docker, images, containers, Compose

The oldest pain in software: it works on one machine and breaks on another, because the machines differ in a thousand small ways. Cargo shipping had the same problem until the standard steel container: pack anything inside, and every ship, crane, and truck handles it identically.

**Docker** is that standard for software. An **image** is a frozen package containing a program plus everything it needs (its libraries, settings, even its own slice of an operating system). A **container** is a running instance of an image, isolated from the rest of your machine. Same image → same behavior, everywhere. Delete the container and your machine is exactly as before.

**Docker Compose** starts several containers together from one description file (`docker-compose.yml`) — essential once a lab needs a database *and* a web server *and* a cache at the same time.

### Python

**Python** is a programming language designed to read close to plain English, which makes it the right tool for this course's small demonstrations. A **script** is a small program in one file, run directly. We will use scripts to *feel* things: how much slower disk is than memory, how a hash ring redistributes keys, how a rate limiter says no.

### curl, DNS and dig, JSON and jq

- **curl** sends a web request from the terminal and shows the raw, unfiltered reply — everything your browser hides. It is how we will dissect the web's machinery.
- **DNS** is the internet's phone book: it turns names like `google.com` into the numeric addresses computers actually use. (Lesson 07 covers it fully.) **dig** is the standard tool for asking DNS questions. Windows lacks dig natively; the built-in **nslookup** covers the basics, and the real dig will run from a Docker container when the DNS lab arrives.
- **JSON** is the standard text format web services use to exchange data — readable, but often delivered as one endless line. **jq** pretty-prints and filters it.
- A **pipe** (`|`) feeds the output of one command into the next as input: `curl ... | jq .` means "fetch, then prettify."

### Course conventions

- **Markdown** (`.md` files): plain text with light markup (`#` heading, `**bold**`), rendered by GitHub as formatted pages. All lessons and design docs use it.
- **ASCII diagrams**: pictures drawn with text characters, for quick inline structure.
- **Mermaid diagrams**: text that GitHub renders into real boxes-and-arrows graphics — architecture, sequences, data models. Your committed portfolio looks like a portfolio.
- **`glossary.md`** — every term, one line, with its lesson number. **`toolkit.md`** — the numbers, formulas, and decision tables of the trade; the file you reread before any real design. **`troubleshooting.md`** — decodes lab errors. All three grow for the rest of the course.

---

## SECTION 4 — HOW IT WORKS UNDERNEATH

What actually happens when you run the install and verify commands:

1. `winget install <name>` — winget looks the name up in Microsoft's public package catalog, downloads the installer from the vendor's official source, checks its integrity, and runs it silently. That's why a new terminal is needed afterward: the list of folders the shell searches for programs (the **PATH**) is read once at terminal startup, so a program installed a minute ago is only found by a *freshly opened* terminal.
2. `docker run hello-world` — the Docker client asks the Docker engine (the background service Docker Desktop runs) for an image called `hello-world`. The engine doesn't have it, so it downloads it from Docker Hub (the public warehouse of images), creates an isolated container from it, runs the tiny program inside, streams its output to your terminal, and — because of `--rm` — deletes the container. One command exercised the entire pipeline: registry → download → isolate → run → clean up.
3. `git log --oneline` — Git reads the `.git` folder inside this directory (that folder *is* the repository's memory) and prints one line per commit, newest first.
4. `nslookup google.com` — your machine sends a tiny question ("what address is google.com?") over the network to a DNS server and prints the numeric addresses that come back. Lesson 07 traces this journey hop by hop.

---

## SECTION 5 — HANDS-ON LAB: install and verify everything

Run each block in PowerShell. Compare what you see with each prediction — if they differ, the machine is right; note what you saw.

**1. Package manager**
```powershell
winget --version
```
*Prediction:* a version like `v1.11.xxx`. Any version = working.

**2. Git (already installed and configured — just verify)**
```powershell
git --version
git log --oneline
```
*Prediction:* `git version 2.5x.x.windows.1` (any 2.4x+ fine), then `6a351ff chore: initial course setup`.

**3. Docker Desktop**
```powershell
winget install Docker.DockerDesktop
```
Restart the computer, launch **Docker Desktop** from the Start menu, wait for it to say "running", then:
```powershell
docker --version
docker compose version
docker run --rm hello-world
```
*Prediction:* `Docker version 28.x.x`, `Docker Compose version v2.x.x`, then a message beginning `Hello from Docker!` explaining the steps it just performed. `error during connect` means the Docker Desktop app isn't running yet.

**4. Python 3**
```powershell
winget install Python.Python.3.14
```
Open a **new** terminal, then:
```powershell
python --version
```
*Prediction:* `Python 3.14.x`. If the Microsoft Store opens instead, see `troubleshooting.md`.

**5. curl (built in)**
```powershell
curl.exe --version
```
*Prediction:* `curl 8.x.x` plus a feature list. Always type `curl.exe` in PowerShell — bare `curl` is an alias for a different command.

**6. DNS lookup (built in)**
```powershell
nslookup google.com
```
*Prediction:* a server line or two, then `Name: google.com` and one or more `Address:` lines with numbers like `142.250.x.x`.

**7. jq**
```powershell
winget install jqlang.jq
```
New terminal, then:
```powershell
echo '{"course":"system design","lesson":0}' | jq .
```
*Prediction:*
```json
{
  "course": "system design",
  "lesson": 0
}
```

If every block matched its prediction, your workshop is ready.

---

## SECTION 6 — IN SYSTEM DESIGN

Even a setup lesson carries design lessons:

- **Reproducibility is a design value.** Docker exists because "works on my machine" is not good enough at scale — production systems must behave identically across hundreds of machines. Pinning image versions (which we will do in every `docker-compose.yml`) is the same discipline applied to labs.
- **History is a design value.** Git's append-only history is the same idea behind database write-ahead logs and event sourcing, which you will meet later: never overwrite the past, record every change, and any state can be reconstructed.
- **Secrets never enter history.** The `.gitignore` rule for `.env` is your first security decision: anything committed is copied, forever, everywhere the repo goes.
- **Text beats clicking.** Every tool today is command-line-first because commands can be saved, repeated, reviewed, and automated. Infrastructure-as-code (Lesson 82) is this idea grown up.

---

## SECTION 7 — GOTCHAS AND COMMON MISTAKES

- **Testing a tool in the same terminal that installed it.** The PATH is read at terminal startup, so the shell can't find the new program. Always open a fresh terminal after installing. People hit this constantly because nothing tells you to.
- **Running `docker` before Docker Desktop is running.** The `docker` command is only a messenger; the engine inside Docker Desktop does the work. `error during connect` almost always means "the app isn't started," not "the install failed."
- **Typing `curl` instead of `curl.exe` in PowerShell.** PowerShell aliases `curl` to its own `Invoke-WebRequest`, which takes different options and gives different output. The `.exe` suffix forces the real curl.
- **Letting the Microsoft Store hijack `python`.** Windows ships a fake `python` command that opens the Store. Fix in `troubleshooting.md`.
- **Committing files that should stay private.** `git add .` is safe here *only because* `.gitignore` was written first. Writing the ignore file before the first `add` is the habit; adding secrets "just for a second" is how leaks happen.

---

## SECTION 8 — TRADEOFFS AND ALTERNATIVES

- **Docker Desktop** is free for personal/educational use but licensed for large companies; alternatives (Podman, Rancher Desktop) exist and speak the same commands. We use Docker Desktop because it is the smoothest path on Windows, and everything you learn transfers.
- **winget vs. manual installers vs. Chocolatey/Scoop.** Any of them works. winget wins here because it ships with Windows — zero extra setup.
- **nslookup vs. dig.** nslookup is built in but less detailed; dig shows the full anatomy of a DNS answer. We accept nslookup now and get real dig via Docker in Lesson 07 — a deliberate "good enough now, right tool when it matters" tradeoff.
- **Local Docker vs. cloud accounts.** The course prefers free and local. The cloud lessons (Phase 4) will say clearly when something can only be shown on real cloud and what it costs.

---

## SECTION 9 — KEY TAKEAWAYS

- The terminal is where real engineering happens, because typed commands are precise, repeatable, and work on the screenless servers you will design for.
- Git keeps every version of this course's work forever, and GitHub keeps a copy online; commits after every lesson turn your learning into a visible portfolio.
- Docker packs software plus everything it needs into images that run identically anywhere, which is how this course will hand you real databases and brokers with a single command.
- curl, nslookup/dig, and jq make the invisible machinery of the web visible, so you can verify claims instead of trusting them.
- Files that must not be public — private course files and above all secrets — are excluded by `.gitignore` *before* the first commit, because Git history is permanent.

---

## SECTION 10 — CHALLENGE WITH HIDDEN ANSWER

Using only commands from this lesson: fetch `https://api.github.com/zen` (an address that returns a short motto) with the real curl, and then explain what would be different about running it twice. Then, pipe a request to `https://api.github.com/repos/git/git` through jq to pull out just the `"description"` field. (Hint: jq can select a field with `.fieldname`.)

<details>
  <summary>Click to reveal the answer</summary>

**Part 1:**

```powershell
curl.exe https://api.github.com/zen
```

This prints a short motto such as `Practicality beats purity.` Running it twice usually prints a *different* motto — the server picks one at random per request. That's a first taste of an important idea: the same request does not always produce the same response, because the response is generated fresh on the server each time.

**Part 2:**

```powershell
curl.exe -s https://api.github.com/repos/git/git | jq .description
```

*Prediction:* `"Git Source Code Mirror ..."` (the repo's one-line description, in quotes).

How it works: curl fetches a large JSON document describing the repository; the pipe hands that text to jq; `.description` tells jq to discard everything except the `description` field. The `-s` flag means "silent" — it hides curl's progress meter so only the JSON travels down the pipe.

</details>

---

## SECTION 11 — TOOLKIT UPDATE

Nothing numeric yet — `toolkit.md` is seeded today with its skeleton (sections for latency numbers, powers of two, estimation formulas, and decision tables), ready for Lesson 02 and Lesson 03 to fill in the first real entries.

---

## SECTION 12 — WHAT IS NEXT

Lesson 01 begins the real material: what "designing a system" actually means, why it is a discipline of tradeoffs rather than code, and the repeatable way to approach any design problem — including the questions to ask before drawing a single box.

---

*Lesson 00 of 110 · Phase 0, Chapter 00 (Setup) — chapter complete after this lesson*
