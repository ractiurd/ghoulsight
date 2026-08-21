<div align="center">

# GhoulSight

[![Go Version](https://img.shields.io/badge/Go-1.25+-00ADD8?style=flat-square&logo=go)](https://go.dev)
[![License](https://img.shields.io/badge/License-Proprietary-red?style=flat-square)](LICENSE)
[![Platform](https://img.shields.io/badge/Platform-Linux-FCC624?style=flat-square&logo=linux)]()

**Precision XSS Detection. Real Findings. Zero Noise.**

> *GhoulSight Walks the Graveyard — XSS That Moves Leaves a Shadow*

</div>

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
```


---

## Usage


### Command-Line Flags

#### Target

| **Flag** | **Description** |
| --- | --- |
| `-u <url>` | Single URL to scan, or crawl root when used with `-crawl` |
| `-l <file>` | URL list file (one URL per line) |
| `-r <file>` | Load raw HTTP request from file (sqlmap-style) |
| `--domain <domain>` | Domain to crawl and automatically discover URLs |
| `-crawl` | Treat the `-u` target as a crawl root |
| `stdin` | Pipe URLs via standard input |

#### Scan Options

| **Flag** | **Description** |
| --- | --- |
| `-m <mode>` | Scan mode: `r`, `d`, `c`, or `f` (default: `r`) |
| `--file <path>` | Custom payload file or folder |
| `-t <int>` | Concurrent threads (default: `10`) |
| `-T, --timeout <int>` | Request timeout in seconds (default: `15`) |
| `--depth <int>` | Crawl depth (default: `2`) |
| `-v, --verbose` | Show detailed scan progress |
| `-o <file>` | Save scan results to file |
| `-p, --probe` | Probe URLs before scanning (default: `true`) |
| `--rc` | Reflection check only (no XSS testing) |
| `--resume <file>` | Resume an interrupted scan from a checkpoint |
| `--checkpoint <file>` | Custom checkpoint file path (default: `<outfile>.ckpt.json`) |
| `--no-checkpoint` | Disable writing the scan checkpoint |
| `--cpu <int>` | Maximum CPU usage percentage (default: `60`) |

#### Network

| **Flag** | **Description** |
| --- | --- |
| `--cookies <str>` | Custom cookies (e.g., `'session=abc; token=xyz'`) |
| `-H <str>` | Custom HTTP headers (e.g., `'Authorization: Bearer tok'`) |
| `--data <str>` | Form data for POST scanning (e.g., `'user=test'`) |

#### Fuzzing

| **Flag** | **Description** |
| --- | --- |
| `--fuzz-mode <mode>` | Attack mode: `single`, `cluster`, or `pitchfork` (default: `single`) |
| `--fuzz-replace <kw>` | Custom FUZZ keyword (default: `FUZZ`) |

#### Notifications & Activation

| **Flag** | **Description** |
| --- | --- |
| `--telegram` | Set up Telegram bot notifications interactively |
| `--activate <key>` | Activate subscription using an activation key |

#### Web Server & Chrome

| **Flag** | **Description** |
| --- | --- |
| `--web` | Start the GhoulSight web server interface |
| `--chrome` | Launch Chrome for live traffic interception and URL collection |
| `--port <int>` | Web server port (default: `8080`) |

### Scan Modes

| **Mode** | **Name** | **Description** |
| --- | --- | --- |
| `r` | Reflected | Traditional reflected XSS scanning, including POST form scanning |
| `d` | DOM | DOM-based XSS scanning |
| `c` | Context-Aware | AI-powered context detection and intelligent payload generation |
| `f` | Fuzz | FUZZ keyword-based scanning (ffuf-style) |

> **Note:** Only one scan mode can be selected per run.

### Examples

```bash
# Scan a single URL
./ghoulsight -u "https://example.com/page?id=1" -m c

# Scan URLs from a file
./ghoulsight -l urls.txt -m r --file payloads.txt -o results.txt

# Crawl and scan a domain
./ghoulsight --domain example.com --depth 3 -m d -v

# Use a target as a crawl root
./ghoulsight -u example.com -crawl --depth 3 -m r -v

# Scan a raw HTTP request
./ghoulsight -r request.txt --file payloads.txt -v -o results.txt

# FUZZ keyword-based scanning
./ghoulsight -u "https://example.com/api/FUZZ/users" -m f --fuzz-mode cluster

# Start the web server
./ghoulsight --web --port 8080

# Launch Chrome for live traffic interception and scanning
./ghoulsight --chrome -m r
```


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

| Feature | GhoulSight | Dalfox | XSStrike | XSS0r |
|---------|:---:|:---:|:---:|:---:|
| Browser‑verified (zero false positives) | ✅ | ❌ | ❌ | ✅ |
| Web UI with bulk scan queue | ✅* | ❌ | ❌ | ❌ |
| Persistent result storage | ✅* | ❌ | ❌ | ❌ |
| Path‑based XSS detection | ✅ | ✅ | ❌ | ✅ |
| Context‑aware payload generation | ✅ | ✅ | ✅ | ❌ |
| Checkpoint & resume | ✅* | ❌ | ❌ | ✅ |
| Browser extension support | ✅* | ❌ | ❌ | ❌ |
| Direct browser integration | ✅* | ❌ | ❌ | ❌ |

> \*Available in the **full version** – see Licensing for details.

GhoulSight combines all these features into one professional, easy‑to‑use tool, and remains actively maintained.

---
## 📊 Subscription Plans

Choose the plan that fits your needs. **100% of every subscription fee is donated directly to the Palestinian people.**

| Feature |  Trial |  Pro |
|---------|:---:|:---:|
| **Price** | Free | $5/month |
| **CLI Scans** | 50 runs | Unlimited |
| **Web Interface** | 1-hour sessions | Unlimited |
| **Reflected XSS** | ✅ | ✅ |
| **DOM‑Based XSS** | ✅ | ✅ |
| **Context‑Aware (AI)** | ✅ | ✅ |
| **Fuzz Scanning** | ✅ | ✅ |
| **Domain Crawling** | ✅ | ✅ |
| **Path‑Based XSS** | ✅ | ✅ |
| **Browser Extension** | ❌ | ✅ |
| **Web UI Dashboard** | ❌ | ✅ |
| **Bulk Scan Queue** | ❌ | ✅ |
| **Checkpoint & Resume** | ✅ | ✅ |
| **Advanced WAF Evasion** | ✅ | ✅ |


---

### 🔑 Activation

```bash
# Start interactive activation
./ghoulsight --activate

# Activate with your key
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

---

<div align="center">

## 🇵🇸 We Stand with Palestine

**100% of every subscription fee will be donated directly to the Palestinian people.**

</div>

---

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

<p align="center">
  <sub>Built with ❤️ by <a href="https://t.me/ractiurd">Ractiurd</a></sub>
</p>

---


