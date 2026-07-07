# Glossary

Every term introduced in the course, in plain language, with the lesson where it first appeared. This is an index for looking things up later — the full explanation always lives in the lesson itself.

| Term | Plain-language meaning | First appeared |
|---|---|---|
| Terminal | A program where you type text commands and the computer answers in text. | Lesson 00 |
| Shell | The program inside a terminal that reads your command and decides what to do with it (PowerShell on Windows). | Lesson 00 |
| Package manager | A tool that installs software with one typed command instead of download-and-click (winget on Windows). | Lesson 00 |
| PATH | The list of folders the shell searches to find a program you name; read once when a terminal opens. | Lesson 00 |
| Version control | Keeping every saved snapshot of a project so any earlier state can be restored. | Lesson 00 |
| Git | The universal version-control tool. | Lesson 00 |
| Repository (repo) | A folder tracked by Git: the files plus their entire history. | Lesson 00 |
| Commit | One saved snapshot in Git, with a message describing what changed. | Lesson 00 |
| GitHub | A website that stores an online copy of a Git repository — backup plus public portfolio. | Lesson 00 |
| Remote | The online copy of your repository, from the local repo's point of view. | Lesson 00 |
| Push | Sending your new local commits up to the remote. | Lesson 00 |
| .gitignore | A list of files Git must never record (private files, secrets). | Lesson 00 |
| Docker | A tool that packs a program plus everything it needs into a standard unit that runs identically on any machine. | Lesson 00 |
| Image (Docker) | The frozen package: a program with all its dependencies, ready to run. | Lesson 00 |
| Container | A running instance of an image, isolated from the rest of the machine. | Lesson 00 |
| Docker Compose | Docker's companion that starts several containers together from one description file. | Lesson 00 |
| Docker Hub | The public online warehouse of Docker images. | Lesson 00 |
| Python | A programming language designed to read close to plain English; used for this course's small experiments. | Lesson 00 |
| Script | A small program in a single file, run directly. | Lesson 00 |
| curl | A terminal tool that sends a web request and shows the raw reply, with nothing hidden. | Lesson 00 |
| DNS | The internet's phone book: turns names like google.com into the numeric addresses computers use. (Fully covered in Lesson 07.) | Lesson 00 |
| dig | The standard terminal tool for asking DNS questions. | Lesson 00 |
| nslookup | Windows' built-in, simpler cousin of dig. | Lesson 00 |
| JSON | The standard text format web services use to exchange data. | Lesson 00 |
| jq | A terminal tool that pretty-prints and filters JSON. | Lesson 00 |
| Pipe (`\|`) | Feeds the output of one command into the next command as input. | Lesson 00 |
| Markdown | Plain text with light markup (`#` = heading) that GitHub renders as formatted pages. | Lesson 00 |
| ASCII diagram | A picture drawn with text characters, for quick inline structure. | Lesson 00 |
| Mermaid diagram | A text description that GitHub renders into a real boxes-and-arrows graphic. | Lesson 00 |
| System | A set of parts (servers, databases, caches, queues, network) that work together to do a job. | Lesson 01 |
| System design | Deciding what the parts of a system are, how they connect, and how data flows, so the whole meets its goals under real-world pressure. | Lesson 01 |
| Tradeoff | A choice where improving one thing forces another thing to get worse; naming the cost of every choice is the core skill. | Lesson 01 |
| Functional requirement | What the system does — a feature, phrased "the user can ___". | Lesson 01 |
| Non-functional requirement | How well the system does it — a quality, not a feature (scale, latency, availability, consistency, cost). | Lesson 01 |
| Latency | The delay between asking for something and getting it — the wait; measured in milliseconds. (Numbers in Lesson 03.) | Lesson 01 |
| Availability | The fraction of time a system is up and answering, measured in "nines" (99.9% ≈ 8.7 hrs downtime/year). (Full in Lesson 04.) | Lesson 01 |
| Consistency | Whether all copies of the data agree right now; strong = always identical, eventual = agrees after a short delay. (Full in Lesson 39.) | Lesson 01 |
| Strong consistency | Every reader sees the same, latest value at the same instant (e.g. a bank balance). | Lesson 01 |
| Eventual consistency | Copies may briefly disagree but converge shortly after (e.g. a like count). | Lesson 01 |
| Clarifying question | A question asked before designing, to narrow scope and pin down scale and constraints. | Lesson 01 |
| Capacity estimation | Back-of-the-envelope math (requests/sec, storage, bandwidth) to size a system. (Full in Lesson 02.) | Lesson 01 |
