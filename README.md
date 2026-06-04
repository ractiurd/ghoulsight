<div align="center">

## FREE PALESTINE

**Israel is a rogue terrorist state committing genocide in Gaza. Ethnic cleansing. Mass murder of women, children, and civilians.**
**Bombing hospitals. Destroying homes. Starving an entire population. Erasing entire bloodlines from existence.**
**Now attacking Lebanon. Now striking Iran. All backed, funded, and armed by the United States of America.**
**Two terror states working together — one drops the bombs, the other signs the checks.**

**This is not self-defense. This is apartheid. This is occupation. This is terrorism sponsored by a superpower.**
**The world watches. The world stays silent. We will not.**
**Every government that shakes hands with Israel has blood on its hands. Every politician who stays silent is complicit.**
**No amount of Western media propaganda will wash away the blood of tens of thousands of innocent Palestinians.**
**Remove the blanket from your eyes. Stop believing the lies fed to you by corrupt media. Verify the facts yourself.**
**Open your eyes — the evidence is everywhere. The mass graves. The flattened cities. The children buried under rubble.**
**This is real. This is happening now. And your silence makes you part of it.**
**Boycott every company that funds this genocide. Boycott every product that feeds this war machine.**
**Your money is their weapons. Stop funding your own humanity's destruction.**
**Stand up. Speak out. Or history will remember you as the ones who watched and did nothing.**
**Donate as much as you can. Every dollar feeds a starving child. Every donation rebuilds a destroyed home. Every contribution saves a life.**

**WE STAND WITH PALESTINE.**

From the river to the sea, Palestine will be free.

</div>

---

<div align="center">

```
 ██████╗ ██╗  ██╗ ██████╗ ██╗   ██╗██╗     ███████╗██╗ ██████╗ ██╗  ██╗████████╗
██╔════╝ ██║  ██║██╔═══██╗██║   ██║██║     ██╔════╝██║██╔════╝ ██║  ██║╚══██╔══╝
██║  ███╗███████║██║   ██║██║   ██║██║     ███████╗██║██║  ███╗███████║   ██║   
██║   ██║██╔══██║██║   ██║██║   ██║██║     ╚════██║██║██║   ██║██╔══██║   ██║   
╚██████╔╝██║  ██║╚██████╔╝╚██████╔╝███████╗███████║██║╚██████╔╝██║  ██║   ██║   
 ╚═════╝ ╚═╝  ╚═╝ ╚═════╝  ╚═════╝ ╚══════╝╚══════╝╚═╝ ╚═════╝ ╚═╝  ╚═╝   ╚═╝   
```

### Ghoulsight Walks the Graveyard — XSS That Moves, Leaves a Shadow

[![Go Version](https://img.shields.io/badge/Go-1.25+-00ADD8?style=flat-square&logo=go)](https://go.dev)
[![License](https://img.shields.io/badge/License-MIT-yellow?style=flat-square)](LICENSE)
[![Platform](https://img.shields.io/badge/Platform-Linux-FCC624?style=flat-square&logo=linux)]()

**Advanced XSS Scanner with Zero False Positives**

[Features](#-features) · [Installation](#-installation) · [Usage](#-usage) · [Modes](#-scan-modes) · [License](#-licensing)

</div>

---

## Overview

GhoulSight is a high-performance XSS vulnerability scanner that combines traditional scanning techniques with advanced payload generation to deliver **verified results with zero false positives**. Unlike other scanners that rely solely on reflection detection, GhoulSight validates every XSS finding through real execution.

> **Original Script:** Nishan Fiyaz  
> **Rebuilt & Upgraded:** Mahedi Hasan ([@ractiurd](https://t.me/ractiurd))

---

## Features

### Core Scanner
- **Verified Results** — Every XSS finding is verified through real execution, eliminating false positives entirely
- **Smart Scan** — Stops testing a URL after the first confirmed XSS is found, saving time and resources
- **Multi-Mode Scanning** — Reflected, DOM, Context-Aware, and Fuzz modes (run individually or combined)
- **URL Probing** — Pre-validates URLs before scanning to skip dead targets
- **Reflection Cache** — Caches reflection results to avoid redundant parameter testing
- **Two-Phase Scanning** — Custom payloads first, then falls back to default payloads for URLs with no findings

### Context-Aware Engine (Mode `c`)
- **AI-Powered Context Detection** — Analyzes injection context (HTML attribute, JavaScript, CSS, URL, etc.) and generates context-specific payloads
- **Mutation Engine** — Automatically applies encoding, syntax, breakout, grammar, and interaction-based mutations to maximize bypass rates
- **Adaptive Learning** — Tracks successful mutation patterns across scans, learns WAF bypass techniques, and persists knowledge for future runs


### Fuzz Scanner (Mode `f`)
- **FUZZ Keyword Support** — Replace any part of a URL, header, cookie, or form data with `FUZZ` for position-specific testing
- **Attack Modes** — Single, Cluster Bomb, and Pitchfork (ffuf-style multi-position fuzzing)
- **Auto-Detection** — Automatically switches to fuzz mode when `FUZZ` keyword is detected

### Crawling & Discovery
- **Domain Crawler** — Automatically discovers URLs with parameters from a target domain
- **Configurable Depth** — Crawl depth control (default: 2)
- **Form Extraction** — Discovers and tests GET/POST form parameters
- **Link Discovery** — Extracts links from `href`, `src`, `action`, `data-url`, `data-href` attributes

### Path-Based XSS Detection
- **Auto-Detection** — Automatically detects when URL path segments reflect input in the response
- **Path Segment Injection** — Injects payloads into URL path segments (not just query parameters)
- **Smart Path Replacement** — Replaces or appends payloads to the last path segment based on URL structure
- **Batch Processing** — Processes payloads in batches for efficient scanning
- **Multi-Encoding Reflection Check** — Checks for reflection across exact, URL-decoded, URL-encoded, and double-encoded variants

### Input Methods
- Single URL (`-u`)
- URL list file (`-l`)
- Raw HTTP request file (`-r`) — sqlmap-style request parsing
- Domain crawling (`--domain`)
- Stdin piping

### Output & Notifications
- **Real-Time Progress** — Live progress bar with URL count, payload count, and confirmed findings
- **PoC Generation** — Generates ready-to-use Proof of Concept URLs and raw requests
- **Telegram Integration** — Receive real-time scan notifications and confirmed XSS alerts via Telegram bot
- **File Output** — Save all results to file (`-o`)

---

## Installation

### Prerequisites
- **Chromium-based browser** (Google Chrome, Chromium, or Brave must be installed)
- **Linux** (currently supported platform)

> **Note:** GhoulSight requires a Chromium-based browser to be installed on your system. Install via:
> ```bash
> # Debian/Ubuntu
> sudo apt install chromium-browser
> 
> # Arch Linux
> sudo pacman -S chromium
> 
> # Or install Google Chrome
> wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
> sudo dpkg -i google-chrome-stable_current_amd64.deb
> ```

### Download & Run

```bash
# Clone the repository
git clone https://github.com/ractiurd/ghoulsight.git

# Go to the directory
cd ghoulsight

# Make the build executable
chmod +x ghoulsight

# Run it
./ghoulsight -u "https://example.com/page?id=1" -m r
```

### First Run

```bash
# On first run, GhoulSight starts in trial mode (300 trial runs)
./ghoulsight -u "https://example.com/page?id=1" -m r

# To activate a subscription:
./ghoulsight --activate
```

---

## Usage

```
USAGE:
    ghoulsight -u <url> -m <mode> [options]
    ghoulsight -l <file> -m <mode> [options]
    ghoulsight --domain <domain> --depth 3 -m r,d,c
    ghoulsight -r request.txt --file payloads.txt -v
    ghoulsight --activate <key>

TARGET:
    -u <url>              Single URL to scan
    -l <file>             URL list file
    -r <file>             Load raw HTTP request from file (sqlmap-style)
    --domain <domain>     Domain to crawl (auto-discovers URLs)
    stdin                 Pipe URLs via stdin

SCAN OPTIONS:
    -m <mode>             Scan mode(s): r, d, c, f (comma-sep, default: r)
    --file <path>         Custom payload file or folder
    -t <int>              Concurrent threads (default: 10)
    -T, --timeout <int>   Request timeout in seconds (default: 15)
    --depth <int>         Crawl depth (default: 2)
    -v, --verbose         Show detailed scan progress
    -o <file>             Save results to file
    -p, --probe           Probe URLs before scanning (default: true)
    --rc                  Reflection check only (no XSS testing)

NETWORK:
    --cookies <str>       Custom cookies (e.g., 'session=abc; token=xyz')
    -H <str>              Custom headers (e.g., 'Authorization: Bearer tok')
    --data <str>          Form data for POST scanning (e.g., 'user=test')

FUZZING:
    --fuzz-mode <mode>    Attack mode: single, cluster, pitchfork (default: single)
    --fuzz-replace <kw>   Custom FUZZ keyword (default: FUZZ)

NOTIFICATIONS:
    --telegram            Setup Telegram bot notifications (interactive)
    --activate <key>      Activate subscription with activation key
```

---

## Scan Modes

| Mode | Flag | Description |
|------|------|-------------|
| **Reflected** | `r` | Traditional reflected XSS scanning. Includes POST form parameter testing. |
| **DOM** | `d` | DOM-based XSS detection — analyzes page DOM for vulnerable sinks and sources. |
| **Context-Aware** | `c` | AI-powered context detection. Analyzes injection context and generates context-specific payloads with mutation engine. Includes both GET and POST parameter testing. |
| **Fuzz** | `f` | FUZZ keyword-based position scanning (ffuf-style). Supports single, cluster bomb, and pitchfork attack modes. |

Modes can be combined: `-m r,d,c` runs reflected, DOM, and context-aware scans simultaneously.

---

---

## Payloads

GhoulSight **does not** come with built-in default payloads. You must provide your own payload files.

Payload files are stored in `~/.config/ghoulsight/payloads/`:

```
~/.config/ghoulsight/payloads/
├── reflected/    # Reflected XSS payloads
├── dom/          # DOM XSS payloads
└── post/         # POST form payloads
```

Specify your payloads with `--file`:
```bash
# Single payload file
ghoulsight -u 'https://target.com' --file custom_payloads.txt

# Payload folder
ghoulsight -u 'https://target.com' --file ./my_payloads/
```

> **Note:** The Context-Aware mode (`-m c`) generates payloads dynamically and does not require a payload file.

---

## Licensing

GhoulSight uses a subscription-based licensing model.

> **100% of subscription proceeds go directly to Palestinian people.** By purchasing a license, you are not just supporting this tool — you are feeding a family, treating a wound, rebuilding what was destroyed.

### Trial Mode
- **300 trial runs** on first installation — no activation required
- Each run decrements the trial counter
- Trial runs are preserved when activating a subscription

### Subscription
- **30-day license** per activation
- Activation is machine-bound
- To activate:
  1. Run `./ghoulsight --activate`
  2. Send the displayed **Request Key** to [@ractiurd](https://t.me/ractiurd) on Telegram
  3. Receive your **Activation Key** and enter it when prompted

```bash
# Interactive activation
./ghoulsight --activate

# Activate with key (after receiving from admin)
./ghoulsight --activate <activation_key>
```

### Status Display

| Status | Meaning |
|--------|---------|
| `SUBSCRIPTION ACTIVE` | Valid license — full access, trial counter preserved |
| `TRIAL MODE` | No license installed — using trial runs |
| `SUBSCRIPTION EXPIRED` | License expired — falls back to remaining trial runs |
| `LICENSE EXPIRED` | No trial runs remaining — activation required |

---

## Features Not Included in Public Release

The following features are available in the **full version** and have been **removed** from this public release:

| Feature | Description |
|---------|-------------|
| **Web Server** | Built-in web server for hosting scan results and managing scans remotely (`--web --port 8080`) |
| **Web UI Dashboard** | Browser-based interface for scan management, result viewing, and real-time monitoring |
| **Chromium Extension** | Browser extension for in-page XSS testing and manual payload injection |
| **Advanced WAF Evasion** | Enhanced WAF bypass techniques with automatic payload transformation |

For access to the full version, contact [@ractiurd](https://t.me/ractiurd).

---

## Technical Details

- **Language:** Go 1.25
- **Concurrency:** Thread-pooled scanning with configurable concurrency (`-t`)
- **Adaptive Learning:** Persistent mutation success tracking across sessions
- **Network Resilience:** Automatic retry on network interruptions

---

<div align="center">

**GhoulSight** — XSS That Moves, Leaves a Shadow

</div>
