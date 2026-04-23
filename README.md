# 🛡️ Clawpilot Skills

> Custom AI skills for **Clawpilot** — a desktop AI copilot for Microsoft Security specialists

![Skills](https://img.shields.io/badge/skills-1-blue?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)
![Clawpilot](https://img.shields.io/badge/clawpilot-v1.0.0%2B-0078D4?style=flat-square)

---

## 🤖 What is Clawpilot?

**Clawpilot** is a desktop AI assistant with deep integration into Microsoft 365, browser automation, and an extensible skill system. Skills are slash-command-triggered instruction sets that orchestrate multi-tool workflows — combining web research, internal intelligence, file generation, and diagram creation into a single conversational experience. Think of it as GitHub Copilot, but for your entire desktop workflow.

---

## 📦 Available Skills

| Skill | Command | Description |
|---|---|---|
| [**Compete**](./compete/) | `/compete [vendor]` | Deep cybersecurity competitive analysis — Microsoft Security vs any vendor. Feature tables, AI security deep dive, pricing TCO, architecture diagrams, and optional Excel/Word/PowerPoint exports. |

---

## 🚀 Quick Start

### Prerequisites

- [Clawpilot](https://github.com/clawpilot) desktop app installed and running
- Microsoft 365 account (for internal intelligence gathering)
- Internet access (for web research)

### Installation

#### Option 1: Copy a single skill

**Windows (PowerShell)**
```powershell
xcopy /E /I "compete" "%USERPROFILE%\.copilot\m-skills\compete"
```

**macOS / Linux (Terminal)**
```bash
# Create the skills directory if it doesn't exist
mkdir -p ~/.copilot/m-skills

# Copy the skill
cp -r compete ~/.copilot/m-skills/compete
```

#### Option 2: Clone the entire repo

**Windows (PowerShell)**
```powershell
git clone https://github.com/Itaiaharonov/clawpilot-skills.git
cd clawpilot-skills

# Install all skills at once
for /d %s in (*) do if exist "%s\skill.json" xcopy /E /I "%s" "%USERPROFILE%\.copilot\m-skills\%s"
```

**macOS / Linux (Terminal)**
```bash
git clone https://github.com/Itaiaharonov/clawpilot-skills.git
cd clawpilot-skills

# Create the skills directory if it doesn't exist
mkdir -p ~/.copilot/m-skills

# Install all skills at once
for skill in */; do
  [ -f "${skill}skill.json" ] && cp -r "$skill" ~/.copilot/m-skills/
done
```

#### Option 3: One-liner install (macOS / Linux)

```bash
git clone https://github.com/Itaiaharonov/clawpilot-skills.git /tmp/clawpilot-skills \
  && mkdir -p ~/.copilot/m-skills \
  && cp -r /tmp/clawpilot-skills/compete ~/.copilot/m-skills/ \
  && rm -rf /tmp/clawpilot-skills \
  && echo "✅ /compete skill installed!"
```

#### Option 4: Manual install via Clawpilot UI

1. Open Clawpilot
2. Go to **Settings → Skills → Create New Skill**
3. Name: `compete`
4. Description: Copy from [`compete/skill.json`](./compete/skill.json)
5. Instructions: Copy from [`compete/instructions.md`](./compete/instructions.md)

### ✅ Verify Installation

Type `/compete` in Clawpilot or ask:

```
Can you list my skills?
```

You should see **compete** in the skill catalog.

---

## 🗂️ Skill Structure

Every skill follows the same three-file convention:

```
skill-name/
├── skill.json          # Metadata (name, description, version, triggers)
├── instructions.md     # Full AI instructions (the skill's "brain")
└── README.md           # Human documentation
```

| File | Purpose |
|---|---|
| `skill.json` | Machine-readable metadata — name, version, trigger phrases, required tools |
| `instructions.md` | The prompt that Clawpilot injects when the skill is activated. This defines the entire workflow, rules, and output format. |
| `README.md` | Human-readable docs — what the skill does, how to use it, examples |

---

## 🤝 Contributing

Want to add a new skill? Great — here's how:

1. **Create a folder** with your skill name (lowercase, hyphenated)
2. **Add the three files** (`skill.json`, `instructions.md`, `README.md`)
3. **Test locally** by copying the folder to `~/.copilot/m-skills/`
4. **Open a PR** with a description of what the skill does and example usage

### Guidelines

- Keep `instructions.md` focused and actionable — it's a prompt, not documentation
- Reference sources in `instructions.md` when the skill does research
- Include example invocations in your `README.md`
- Declare all required and optional tools in `skill.json`

---

## 📄 License

[MIT License](./LICENSE) — Copyright © 2026 Itai Aharonov

---

<p align="center">
  Built with ☕ and <strong>Clawpilot</strong>
</p>
