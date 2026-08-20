# GhoulSight

[![Go Version](https://img.shields.io/badge/Go-1.25+-00ADD8?style=flat-square&logo=go)](https://go.dev)
[![License](https://img.shields.io/badge/License-Proprietary-red?style=flat-square)](LICENSE)
[![Platform](https://img.shields.io/badge/Platform-Linux-FCC624?style=flat-square&logo=linux)]()

**Precision XSS Detection. Real Findings. Zero Noise.**

> *GhoulSight Walks the Graveyard — XSS That Moves Leaves a Shadow*

---

## Overview

GhoulSight is built to hunt XSS where others only look.

Designed for security researchers, penetration testers, and bug bounty hunters, it goes beyond basic parameter testing to uncover **Reflected, DOM-based, Context-Aware, Path-Based, POST, and fuzzing attack surfaces**.

GhoulSight maps the target, follows reflections, analyzes injection contexts, mutates payloads, and pushes deeper into the application to uncover vulnerabilities hidden behind complex inputs and filtering.

From a single URL to large-scale target lists and full-domain discovery, GhoulSight is built for one purpose:

**Hunt deeper. Test harder. Find what hides in the shadows.**

*Every reflection leaves a trace. GhoulSight follows it.*

---

## ✨ Features

### Core Scanner
- **Zero False Positives** – Every XSS is triggered in a headless browser before reporting.
- **Smart Scan** – Stops testing a URL after the first confirmed XSS, saving time.
- **Multiple Modes** – Reflected, DOM, Context‑Aware, and Fuzz (can be combined).
- **URL Probing** – Pre‑validates URLs to skip dead targets.
- **Reflection Cache** – Avoids redundant testing of already‑reflected parameters.
- **Two‑Phase Scanning** – Custom payloads first, then fallback to defaults.

### Context‑Aware Engine (Mode `c`)
- **AI‑Powered Context Detection** – Identifies injection context (HTML attribute, JavaScript, CSS, URL, etc.) and generates context‑specific payloads.
- **Mutation Engine** – Automatically applies encoding, syntax, breakout, grammar, and interaction‑based mutations to maximise bypass rates.
- **Adaptive Learning** – Tracks successful mutation patterns across sessions and persists knowledge for future runs.

### Fuzz Scanner (Mode `f`)
- **FUZZ Keyword Support** – Replace any part of URL, header, cookie, or form data with `FUZZ`.
- **Attack Modes** – Single, Cluster Bomb, and Pitchfork (ffuf‑style multi‑position fuzzing).
- **Auto‑Detection** – Automatically switches to fuzz mode when `FUZZ` is detected.

### Crawling & Discovery
- **Domain Crawler** – Discovers URLs with parameters from a target domain.
- **Configurable Depth** – Control crawl depth (default 2).
- **Form Extraction** – Finds and tests GET/POST form parameters.
- **Link Discovery** – Extracts links from `href`, `src`, `action`, `data‑url`, `data‑href`.

### Path‑Based XSS Detection
- **Auto‑Detection** – Recognises when URL path segments reflect input in the response.
- **Path Segment Injection** – Injects payloads into URL path segments (not just query parameters).
- **Smart Replacement** – Replaces or appends payloads to the last segment based on URL structure.
- **Batch Processing** – Processes payloads in batches for efficiency.
- **Multi‑Encoding Reflection Check** – Tests exact, URL‑decoded, URL‑encoded, and double‑encoded variants.

### Input Methods
- Single URL (`-u`)
- URL list file (`-l`)
- Raw HTTP request file (`-r`) – sqlmap‑style parsing
- Domain crawling (`--domain`)
- Stdin piping

### Output & Notifications
- **Real‑Time Progress** – Live progress bar with counts.
- **PoC Generation** – Generates ready‑to‑use Proof‑of‑Concept URLs and raw requests.
- **Telegram Integration** – Receive real‑time scan notifications and confirmed XSS alerts.
- **File Output** – Save results (`-o`) and generate an interactive HTML report.

---

## 📦 Installation

### Prerequisites
- **Linux** (currently supported platform)
- **Chromium‑based browser** (Google Chrome, Chromium, or Brave) – required for headless verification.

```bash
# Debian/Ubuntu
sudo apt install chromium-browser

# Arch Linux
sudo pacman -S chromium

# Or install Google Chrome
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo dpkg -i google-chrome-stable_current_amd64.deb
````

### Download & Run

bash

```
# Clone the repository
git clone https://github.com/ractiurd/GhoulSight.git
cd GhoulSight

# Make the binary executable (if using pre‑built)
chmod +x ghoulsight

# First run – trial mode (300 runs)
./ghoulsight -u "https://example.com/page?id=1" -m r
```

### Build from Source

bash

```
go build -o ghoulsight .
```

---

## 🚀 Usage

bash

```
./ghoulsight -u <url> -m <mode> [options]
./ghoulsight -l <file> -m <mode> [options]
./ghoulsight --domain <domain> --depth 3 -m r,d,c
./ghoulsight -r request.txt --file payloads.txt -v
```

### Command‑Line Flags

#### Target

| **FlagDescription** |                                                |
| ------------------- | ---------------------------------------------- |
| `-u <url>`          | Single URL to scan                             |
| `-l <file>`         | URL list file (one per line)                   |
| `-r <file>`         | Load raw HTTP request from file (sqlmap‑style) |
| `--domain <domain>` | Domain to crawl (auto‑discovers URLs)          |
| `stdin`             | Pipe URLs via stdin                            |

#### Scan Options

| **FlagDescription**   |                                                                  |
| --------------------- | ---------------------------------------------------------------- |
| `-m <mode>`           | Scan mode(s): `r`, `d`, `c`, `f` (comma‑separated, default: `r`) |
| `--file <path>`       | Custom payload file or folder                                    |
| `-t <int>`            | Concurrent threads (default: 10)                                 |
| `-T, --timeout <int>` | Request timeout in seconds (default: 15)                         |
| `--depth <int>`       | Crawl depth (default: 2)                                         |
| `-v, --verbose`       | Show detailed scan progress                                      |
| `-o <file>`           | Save results to file (also generates HTML report)                |
| `-p, --probe`         | Probe URLs before scanning (default: true)                       |
| `--rc`                | Reflection check only (no XSS testing)                           |

#### Network

| **FlagDescription** |                                                      |
| ------------------- | ---------------------------------------------------- |
| `--cookies <str>`   | Custom cookies (e.g., `'session=abc; token=xyz'`)    |
| `-H <str>`          | Custom headers (e.g., `'Authorization: Bearer tok'`) |
| `--data <str>`      | Form data for POST scanning (e.g., `'user=test'`)    |

#### Fuzzing

| **FlagDescription**   |                                                                   |
| --------------------- | ----------------------------------------------------------------- |
| `--fuzz-mode <mode>`  | Attack mode: `single`, `cluster`, `pitchfork` (default: `single`) |
| `--fuzz-replace <kw>` | Custom FUZZ keyword (default: `FUZZ`)                             |

#### Notifications

| **FlagDescription** |                                                |
| ------------------- | ---------------------------------------------- |
| `--telegram`        | Setup Telegram bot notifications (interactive) |
| `--activate <key>`  | Activate subscription with activation key      |

#### Examples

bash

```
# Reflected XSS scan with custom headers
./ghoulsight -u "https://example.com/page?id=1" -m r -H "Authorization: Bearer token"

# DOM scan with verbose output
./ghoulsight -u "https://example.com/search?q=test" -m d -v

# Context‑aware scan with custom payloads
./ghoulsight -u "https://example.com/profile?user=admin" -m c --file ./my_payloads/

# Fuzz scan with cluster bomb mode
./ghoulsight -u "https://example.com/api?param=FUZZ&other=value" -m f --fuzz-mode cluster

# Crawl domain and scan with reflected + DOM
./ghoulsight --domain example.com --depth 3 -m r,d -t 20

# Bulk scan from list file
./ghoulsight -l urls.txt -m r,d,c -o results.txt
```

---

## 🔍 Scan Modes

| **ModeFlagDescription** |     |                                                                             |
| ----------------------- | --- | --------------------------------------------------------------------------- |
| **Reflected**           | `r` | Traditional reflected XSS (GET/POST)                                        |
| **DOM**                 | `d` | DOM‑based XSS detection                                                     |
| **Context‑Aware**       | `c` | AI‑powered dynamic payload generation (does **not** require a payload file) |
| **Fuzz**                | `f` | FUZZ keyword‑based scanning                                                 |

> Modes can be combined: `-m r,d,c` runs all three simultaneously.

---

## 📁 Payload Configuration

GhoulSight does **not** ship with default payloads – you must provide your own.

Payloads are stored in `~/.config/ghoulsight/payloads/`:

text

```
~/.config/ghoulsight/payloads/
├── reflected/    # Reflected XSS payloads
├── dom/          # DOM XSS payloads
└── post/         # POST form payloads
```

You can specify a custom file or folder with `--file`:

bash

```
# Single file
./ghoulsight -u 'https://target.com' --file custom_payloads.txt

# Folder
./ghoulsight -u 'https://target.com' --file ./my_payloads/
```

> **Note:** Context‑Aware mode (`-m c`) generates payloads dynamically and does **not** require a payload file.

---

## 🏆 Comparison with Other XSS Scanners

| **FeatureGhoulSightDalfoxXSStrikeXSS0r** |     |   |   |   |
| ---------------------------------------- | --- | - | - | - |
| Browser‑verified (zero false positives)  | ✅   | ❌ | ❌ | ✅ |
| Web UI with bulk scan queue              | ✅\* | ❌ | ❌ | ❌ |
| Persistent result storage                | ✅\* | ❌ | ❌ | ❌ |
| Path‑based XSS detection                 | ✅   | ✅ | ✅ | ✅ |
| Context‑aware payload generation         | ✅   | ✅ | ✅ | ❌ |
| Checkpoint & resume                      | ✅\* | ❌ | ❌ | ❌ |
| Browser extension support                | ✅\* | ❌ | ❌ | ❌ |
| Direct browser integration               | ✅\* | ❌ | ❌ | ❌ |

> \*Available in the **full version** – see Licensing for details.

GhoulSight combines all these features into one professional, easy‑to‑use tool, and remains actively maintained.

---

## 📜 Licensing

GhoulSight uses a subscription‑based licensing model.

> **100% of every subscription fee is donated directly to the Palestinian people.**
> Every license feeds a family, treats a wound, and helps rebuild destroyed homes.

### Trial Mode

- **300 trial runs** on first installation – no activation required.
- Each run decrements the trial counter.
- Trial runs are preserved when activating a subscription.

### Subscription

- **30‑day license** per activation.
- Machine‑bound activation.
- To activate:
  1. Run `./ghoulsight --activate`
  2. Send the displayed **Request Key** to [@ractiurd](https://t.me/ractiurd) on Telegram.
  3. Receive your **Activation Key** and enter it.

bash

```
# Interactive activation
./ghoulsight --activate

# Activate with key
./ghoulsight --activate <activation_key>
```

### Status Display

| **StatusMeaning**      |                                                      |
| ---------------------- | ---------------------------------------------------- |
| `SUBSCRIPTION ACTIVE`  | Valid license – full access, trial counter preserved |
| `TRIAL MODE`           | No license – using trial runs                        |
| `SUBSCRIPTION EXPIRED` | License expired – falls back to remaining trial runs |
| `LICENSE EXPIRED`      | No trial runs – activation required                  |

---

## 🇵🇸 We Stand with Palestine

\<div align="center"> \<strong>100% of every subscription fee is donated directly to the Palestinian people.\</strong> \</div>

### The Reality We Cannot Ignore

Across Palestine, Lebanon, and Iran, innocent civilians — especially children — are being slaughtered every single day. The United States and Israeli governments are jointly responsible for ongoing bombing campaigns, mass murder, and the systematic destruction of homes, hospitals, schools, and entire neighborhoods.

They drop illegal white phosphorus on densely populated areas. They deploy banned cluster munitions in civilian zones. They fire precision‑guided missiles into refugee camps, schools, and UN shelters. They cut off water, electricity, food, and medicine to millions of men, women, and children. They assassinate journalists, doctors, and aid workers with impunity. They erase entire neighbourhoods, then pretend the world isn’t watching.

> *“They call it ‘defense.’ We call it what it is: ethnic cleansing.”*

### Key Statistics

- 👶 **Over 15,000 children** killed since October 2023
- 🏥 **Hospitals, schools, and UN shelters** deliberately targeted
- 🚫 **Illegal weapons** like white phosphorus used in civilian areas
- 📰 **Journalists and aid workers** assassinated with impunity

### Our Message

- 🏥 Hospitals are not military bases.
- 📰 Journalists are not enemies.
- 👶 Children are not targets.
- ☠️ Genocide is not self‑defense.
- ✋ Ethnic cleansing is not peace.

### Take Action

Every scan you run with GhoulSight helps fund real aid for real people. Your subscription is more than a tool — it’s a stand against genocide.

👉 [**Donate via Subscription**](https://paypal.me/MahediHasan01/5)

Or contact [@ractiurd](https://t.me/ractiurd) on Telegram for alternative payment methods.

---

## 🌐 Full Version (Not in Public Release)

The public release excludes the following features (available in the full version):

- **Web Server & Web UI** – Browser‑based dashboard for scan management and real‑time monitoring (`--web --port`).
- **Chromium Extension** – In‑page XSS testing and manual payload injection.
- **Advanced WAF Evasion** – Enhanced bypass techniques with automatic payload transformation.

For access to the full version, contact [@ractiurd](https://t.me/ractiurd).

---

## 👨‍💻 Credits

- **Original Script:** Nishan Fiyaz
- **Rebuilt & Upgraded:** Mahedi Hasan ([@ractiurd](https://t.me/ractiurd))
- Contact: [@ractiurd](https://t.me/ractiurd) on Telegram

---

## ⚠️ Disclaimer

GhoulSight is intended for **authorised security testing only**. Users are responsible for complying with all applicable laws and obtaining proper authorisation before scanning any target.

---

## 📄 License

This project is **closed‑source** and commercially licensed. Unauthorised distribution, modification, or reverse engineering is prohibited.

---

\<p align="center"> \<sub>Built with ❤️ by \<a href="https\://t.me/ractiurd">Ractiurd\</a>\</sub> \</p> \`\`\`

---

Copy the entire block above, paste it into a new file, and save it as `README.md`.
