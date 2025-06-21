# 🧠 TotalRecon - Advanced PC Information & Forensics Toolkit
![C](https://img.shields.io/badge/c-%2300599C.svg?style=for-the-badge&logo=c&logoColor=white) ![C++](https://img.shields.io/badge/c++-%2300599C.svg?style=for-the-badge&logo=c%2B%2B&logoColor=white) ![C#](https://img.shields.io/badge/c%23-%23239120.svg?style=for-the-badge&logo=csharp&logoColor=white) ![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54) ![PowerShell](https://img.shields.io/badge/PowerShell-%235391FE.svg?style=for-the-badge&logo=powershell&logoColor=white) ![Rust](https://img.shields.io/badge/rust-%23000000.svg?style=for-the-badge&logo=rust&logoColor=white) ![Windows](https://img.shields.io/badge/Windows-0078D6?style=for-the-badge&logo=windows&logoColor=white) ![GitHub](https://img.shields.io/badge/github-%23121011.svg?style=for-the-badge&logo=github&logoColor=white)
 
> A next-generation cross-language, cross-layer system intelligence and digital forensics toolkit powered by Python, Rust, C, C++, C#, and PowerShell.

TotalRecon is an ambitious, ultra-comprehensive utility designed to extract, analyze, and present nearly **every piece of information** about a Windows PC — from basic hardware specs to advanced forensic footprints. Whether you're a power user, forensic analyst, IT professional, or reverse engineer, **TotalRecon** serves as your one-stop diagnostic and telemetry powerhouse.

---

## 🚀 Project Goals

- Provide **complete system visibility** from low-level firmware to high-level user behavior.
- Combine **performance, extensibility, and reliability** using the best features of each programming language.
- Ensure **modular, scriptable, and transparent architecture** — every feature is independently accessible.
- Enable real-time or offline data extraction, with optional JSON/CSV/HTML export support for analysis/reporting.

---

## 🎯 Key Features Overview

### 🖥️ Hardware Intelligence
- **CPU**: Model, cores, threads, architecture, clock speeds, cache sizes
- **GPU**: Model, VRAM, driver version, outputs
- **RAM**: Total memory, module slots, speed, manufacturer
- **Storage**: Devices, SMART data, partitions, usage
- **Motherboard**: Manufacturer, chipset, BIOS version
- **Battery**: Health, design vs current capacity, cycle count
- **Peripherals**: USB devices, scanners, printers

### 🪟 Operating System Insights
- OS version, edition, build number, install date
- Installed and pending **Windows Updates**
- System uptime and boot time
- Environment variables, time zone, locale
- Scheduled tasks, running services
- Installed software with version & install dates

### 👤 User Profile & Activity
- All local and domain **user accounts**
- **Login history** with timestamps and durations
- User privileges (admin vs standard)
- Desktop and Downloads contents
- Recent documents and browser profile metadata

### 🌐 Network Mapping
- IP config, MAC, DNS, gateways, ARP table
- WiFi networks (saved SSIDs, passwords — if admin)
- Open ports and active TCP/UDP connections
- Proxy config, network adapter stats
- Bluetooth and paired device metadata
- VPN and Torrent clients, if detected

### 🔐 Security & Privacy
- Firewall rules, antivirus, Defender history
- BitLocker encryption status
- Login methods (password, PIN, biometrics)
- Credential Manager dump (vaultcmd), SSH/GPG keys
- Installed security certificates
- TPM and Secure Boot status

### 🌍 Geolocation & Physical Context
- Approximate location via public IP
- Nearby WiFi access points
- Time zone and language region info
- Geo-enabled EXIF metadata from media

### 📊 System Performance Metrics
- Real-time and historical CPU, RAM, GPU, disk usage
- Fan speeds, temperatures (if sensors available)
- Active power profile and battery analytics
- Clipboard contents and history (Windows 10/11)

### 🧩 Application Data Extraction
- Installed browsers, extensions, cache, autofill, passwords
- Email clients, office apps, media players
- Game launchers and recent play time
- IDEs and developer environments

---

## 🧰 Technology Stack

This project will leverage multiple languages and tools, each chosen for its strength in a particular domain:

| Language     | Purpose                                                         |
|--------------|-----------------------------------------------------------------|
| **Python**   | Scripting, automation, high-level OS interaction, JSON export   |
| **Rust**     | High-performance, memory-safe hardware-level interrogation      |
| **C/C++**    | Low-level WinAPI access, device control, kernel data extraction |
| **C# (.NET)**| Windows-only GUI (if needed), WMI, registry parsing             |
| **PowerShell** | Native OS commands, security context inspection               |

---

## 📦 Architecture Preview

```plaintext
[ Main Launcher ]
       |
+------+-------+--------+----------+-----------+
|              |        |          |           |
Python      PowerShell  C#       Rust        C/C++
|              |        |          |           |
OS & App   Security  Registry   Hardware   Kernel-Level
Data       Context   Analysis   Probing     Forensics
```

## 🧱 Part 2 - Modular Architecture & Execution Design

TotalRecon is designed as a **modular, multi-language toolkit** where each module performs a focused data extraction task — either locally or in parallel. The system is fully scriptable, allowing individual modules to be executed standalone or orchestrated via a unified controller interface.

---

### 🧩 Core Architectural Principles

- **Language Interoperability**: Components in C, C++, Rust, C#, Python, and PowerShell work independently, with data passed via temporary files, IPC, or subprocess calls.
- **Extensibility First**: New modules can be added without modifying the core engine — just follow the naming and output schema.
- **Clean Data Pipeline**: Each module outputs **structured data** (JSON, CSV, or XML), which is then parsed, logged, or visualized.
- **Cross-Platform-Ready Design** (initial focus on Windows, but prepared for expansion to Linux/macOS).
- **No Admin? No Problem**: The system gracefully falls back to limited-mode operations when administrative privileges are unavailable.

---

### 🧰 Module Breakdown by Layer

Each module is grouped by functionality scope and tech stack:

#### 🖥️ System Hardware Modules (Rust / C / C++)
| Feature | Module | Language | Description |
|--------|--------|----------|-------------|
| CPU Info | `cpu_scan` | Rust | Uses `sysinfo`/`raw_cpuid` for detailed specs |
| GPU Info | `gpu_scan` | C++ | DirectX / WMI queries for GPU/VRAM stats |
| RAM Info | `ram_scan` | Rust | Memory slot info, speed, vendor |
| Storage | `drive_scan` | C | SMART, partitions, disk types |
| Battery | `battery_check` | Rust | Charge cycles, health data |
| Motherboard | `board_id` | C++ | BIOS/UEFI, chipset info via SMBIOS |

#### 🪟 OS and User Data Modules (Python / PowerShell / C#)
| Feature | Module | Language | Description |
|--------|--------|----------|-------------|
| OS Info | `os_info.py` | Python | OS name, build, install date |
| Updates | `win_updates.ps1` | PowerShell | Installed/pending updates |
| Uptime | `uptime.py` | Python | System uptime in human-readable format |
| Environment | `envdump.ps1` | PowerShell | Full environment variable list |
| Installed Software | `programs.ps1` | PowerShell | All apps + install dates |
| Running Services | `services.py` | Python | List and status |

#### 👤 User Behavior and Session Data (Python / C#)
| Feature | Module | Language | Description |
|--------|--------|----------|-------------|
| User Accounts | `users.py` | Python | Local/domain accounts, status |
| Login History | `logins.ps1` | PowerShell | Logon events from Event Viewer |
| Recent Files | `recent_files.py` | Python | Documents, downloads |
| Desktop Scan | `desktop_scan.py` | Python | File inventory on user desktop |
| Clipboard | `clipboard.cs` | C# | Clipboard current content + history (if enabled) |

#### 🌐 Network Forensics Modules (Python / PowerShell)
| Feature | Module | Language | Description |
|--------|--------|----------|-------------|
| IP Config | `netconfig.py` | Python | IPv4/IPv6, subnet, DNS, gateway |
| Open Ports | `ports.py` | Python | `netstat` parsing |
| WiFi | `wifi_profiles.ps1` | PowerShell | Saved SSIDs & passwords |
| Proxy & DNS | `proxy_dns.ps1` | PowerShell | System proxy, DNS settings |
| ARP & Bluetooth | `arp_bt.py` | Python | ARP table + paired Bluetooth |

#### 🔐 Security and Credential Modules (PowerShell / C# / Rust)
| Feature | Module | Language | Description |
|--------|--------|----------|-------------|
| Firewall Rules | `firewall.ps1` | PowerShell | Inbound/outbound rules |
| Antivirus | `antivirus.py` | Python | Defender & 3rd party detection |
| BitLocker | `bitlocker_status.ps1` | PowerShell | Drive encryption state |
| Credential Manager | `vault_dump.cs` | C# | Extract stored credentials |
| TPM | `tpm_status.rs` | Rust | Platform trust info |

#### 🔍 Forensic and Deep State Modules (C++ / Python / Rust)
| Feature | Module | Language | Description |
|--------|--------|----------|-------------|
| Prefetch & Jump Lists | `prefetcher.cpp` | C++ | File execution history |
| Shellbags | `shellbag_parser.rs` | Rust | Folder access artifacts |
| Volume Shadow | `vssdump.py` | Python | Recover deleted data |
| RAM Dump | `ram_forensics.py` | Python | Memory scraping (optional) |
| Clipboard DIB | `clipboard_image_dump.cs` | C# | Restore copied images from memory |

---

### 🔄 Inter-Module Communication

- **Primary Controller**: A Python launcher script acts as the main orchestrator.
- **Data Output Standard**: Every module outputs to a consistent format (`/output/module_name.json`)
- **Scheduling & Threading**: Modules may run synchronously or asynchronously, depending on system load and user config.
- **Security Consideration**: Admin-required modules are clearly marked and skipped in user mode.

---

### 🔧 Execution Modes

| Mode | Description |
|------|-------------|
| **Full Recon** | Runs all available modules and aggregates output into a master report |
| **Module-Only** | Allows targeting one or more modules for testing/debugging |
| **Silent CLI** | Background mode for script automation or enterprise monitoring |
| **GUI/Interactive** (Optional) | Planned for later using WPF (C#) or Tkinter (Python) |

---

### 🗃️ Output Format Example (JSON)
```json
{
  "cpu": {
    "model": "Intel Core i7-12700K",
    "cores": 8,
    "threads": 16,
    "architecture": "x64",
    "clock_speed_ghz": 3.8,
    "l3_cache_mb": 25
  }
}
```

## 🛡️ Part 3 - Data Privacy, Ethical Use & Legal Considerations

Due to the powerful nature of TotalRecon and the sensitive data it can access, it is essential to establish a firm stance on **ethical use, consent, and transparency**. This section outlines the intended scope, responsibilities of the user, and key legal boundaries.

---

### ⚠️ Disclaimer

> **TotalRecon is an advanced system diagnostic and forensic tool designed strictly for ethical, educational, and administrative purposes.**

The author(s) of this tool are **not responsible** for:
- Any misuse or unauthorized deployment of the software.
- Data loss, corruption, or system instability caused by improper usage.
- Violation of local, national, or international cybersecurity laws.

---

### ✅ Intended Use Cases

| Use Case | Description |
|----------|-------------|
| ✅ Personal System Audit | Analyze your own PC for transparency and optimization |
| ✅ Enterprise Asset Inventory | IT admins may use the tool to gather information about organization-owned machines |
| ✅ Forensic Research | Use in digital forensics labs for academic and ethical forensic analysis |
| ✅ Penetration Testing Labs | Red team/blue team simulation in controlled environments |
| ✅ OS & Hardware Compatibility Testing | Evaluate behavior and metadata on various systems |

---

### ❌ Forbidden Use Cases

| Use Case | Reason |
|----------|--------|
| ❌ Monitoring other users without consent | Violates privacy laws and ethical standards |
| ❌ Deployment in malware/rootkits | Unauthorized spying or system compromise |
| ❌ Corporate espionage | Gathering sensitive corporate or competitor data |
| ❌ Nation-state surveillance | Use for government-grade surveillance is prohibited |
| ❌ Unauthorized physical access audits | Running the tool on borrowed/public computers |

---

### 👁️‍🗨️ Transparency Design

TotalRecon will incorporate multiple transparency-focused features to protect user data and promote ethical use:

- 🔓 **Consent Prompting**: When run interactively, users must accept a terms-of-use warning before any scanning begins.
- 📜 **Logging**: Every data extraction action is timestamped and logged locally.
- 🔐 **No Remote Transmission**: This tool does **not** upload any data. Everything remains on the local machine.
- 🛑 **Admin-Only Boundaries**: Features that require elevated privileges are clearly marked and will not execute in limited mode unless overridden with explicit consent.
- 👤 **User-Centric Design**: The tool will respect system group policies and local user settings whenever possible.

---

### 🔒 GDPR / Data Sensitivity Awareness

If you're operating in a region governed by data protection laws like the **General Data Protection Regulation (GDPR)**, **California Consumer Privacy Act (CCPA)**, or similar, you are responsible for:

- Obtaining informed consent before scanning user environments
- Not storing or distributing personally identifiable information (PII) unless permitted
- Keeping user logs encrypted and stored securely
- Providing a way for users to delete or redact their collected data

---

### 📄 License Note (Planned)

TotalRecon will be licensed under a **strict open-source license** (e.g., AGPL or EUPL) that:

- Forces any derivative work or redistribution to disclose their source
- Prevents commercial sale or bundling without explicit approval
- Protects the rights of ethical developers while discouraging misuse

---

### 💡 Best Practices When Using TotalRecon

- Run the tool **only on systems you own or are legally authorized to analyze**
- Always **inform users** in enterprise or team environments
- **Use the JSON output** to redact personal content before public sharing
- Consider encrypting sensitive result files
- Review module output logs regularly for accuracy and compliance

---

> Respect is non-negotiable — building powerful software is a privilege, and using it ethically is a responsibility.

## 📤 Part 4 - Output Format, Reporting & Integration Options

TotalRecon doesn’t just collect data — it presents it in a highly organized, structured, and extensible format suitable for logging, visualization, and automation pipelines. This section outlines how data will be formatted, stored, and optionally visualized or integrated.

---

### 🗂️ Output File Structure

All output data will be saved under a user-defined or default `/output` directory:


/output/  
├── system/  
│ ├── cpu.json  
│ ├── ram.json  
│ ├── gpu.json  
│ └── storage.json  
├── os/  
│ ├── os_info.json  
│ ├── updates.json  
│ └── services.json  
├── user/  
│ ├── accounts.json  
│ ├── login_history.json  
│ ├── clipboard.json  
│ └── recent_docs.json  
├── network/  
│ ├── interfaces.json  
│ ├── wifi.json  
│ └── open_ports.json  
├── security/  
│ ├── firewall.json  
│ ├── antivirus.json  
│ └── credentials.json  
├── forensic/  
│ ├── prefetch.json  
│ ├── shellbags.json  
│ └── jump_lists.json  
└── summary_report.json  


---

### 📊 Data Output Format (JSON Schema)

TotalRecon will standardize all output in human-readable, structured **JSON format**, making it easy to:

- Import into dashboards (e.g., Grafana, Kibana)
- Parse via Python/Pandas for reports
- Convert to other formats like CSV, YAML, or XML

#### ✅ Example: `/output/system/cpu.json`
```json
{
  "timestamp": "2025-06-21T12:00:00+02:00",
  "cpu": {
    "model": "AMD Ryzen 9 7950X",
    "architecture": "x86_64",
    "cores": 16,
    "threads": 32,
    "base_clock_ghz": 4.5,
    "max_clock_ghz": 5.7,
    "l2_cache": "16 MB",
    "l3_cache": "64 MB"
  }
}
```

### 📋 Summary Report

Upon completing a full scan, **TotalRecon** will automatically generate a comprehensive `summary_report.json` containing:

- 🕒 **Scan Timestamp** — Exact date and time the scan was executed  
- ⚠️ **Detected Anomalies** — Any flagged issues or irregularities  
- ✅ **Modules Completed** — Total number of successfully executed modules  
- ❌ **Modules Skipped/Failed** — Modules that were skipped due to permissions, errors, or system limitations  
- 📦 **Optional Archive** — A compressed ZIP archive of all output files for easy sharing or backup  

In addition, an optional, visually enhanced `summary_report.html` will be generated using a pre-built template, presenting a structured dashboard with:

- 🧩 **System Overview** — Quick snapshot of key specs  
- 🖥️ **Hardware Dashboard** — Detailed CPU, GPU, RAM, and storage breakdown  
- 🔐 **Security Posture** — Firewall, antivirus, Defender, and BitLocker status  
- 🌐 **Network Configuration** — IP settings, adapters, open ports, WiFi info  
- 🕵️ **Forensic Flags** — Potential artifacts or digital footprint traces  
  

---

### 📎 Export Formats

To support further analysis, collaboration, or documentation, TotalRecon will support exporting data into multiple formats:

| Format     | Description                                                   |
|------------|---------------------------------------------------------------|
| **CSV**    | Tabular format suitable for Excel, Google Sheets, etc.       |
| **HTML**   | Interactive, user-friendly reports viewable in any browser   |
| **PDF**    | Printable, shareable summaries for documentation or reports  |
| **SQLite** | Structured database for queries and timeline reconstruction  |
| **Markdown** | Plain text summaries ideal for GitHub wikis and reports     |

📌 **Exporting is customizable** — users can enable or disable specific formats via:
- Command-line flags (e.g., `--export-pdf`, `--no-html`)
- GUI toggles (planned)
- Configuration files (`config.yaml` or `settings.json`)

## ⚙️ Part 5 - Execution Modes, Privilege Handling & Interface Design

**TotalRecon** is designed for adaptability. Whether running a complete forensic sweep, performing targeted diagnostics, or integrating with automation pipelines, the tool adjusts to the user’s needs and system permissions.

---

### 🧠 Execution Modes

TotalRecon supports several flexible modes of operation:

| Mode               | Description                                                                 |
|--------------------|-----------------------------------------------------------------------------|
| **Full Scan**       | Executes all modules for a comprehensive system overview                   |
| **Targeted Scan**   | Run specific modules (e.g., CPU, RAM, Network) via CLI flags                |
| **Silent Mode**     | Background execution without prompts or UI — ideal for scripting & automation |
| **Interactive CLI** | Step-by-step prompts for module selection and export options                |
| **GUI Mode** *(Planned)* | Graphical interface for real-time control, visualization, and export management |

> 📁 Output is stored in the `/output` directory by default. Custom paths can be specified using flags or config files.

---

### 🔐 Privilege Handling

TotalRecon will detect the current permission level and adjust behavior accordingly:

| Privilege Level   | Capabilities                                                                 |
|-------------------|------------------------------------------------------------------------------|
| **Administrator**  | Full access to all modules, including advanced diagnostics and secure areas |
| **Standard User**  | Executes only non-restricted modules; others will be skipped with warnings  |
| **Elevation Prompt** | UAC prompt will appear automatically for CLI or GUI when required          |

Each module includes metadata about its privilege requirements and will fail gracefully if those conditions are not met.

---

### 📟 Command-Line Interface (CLI)

TotalRecon’s CLI is optimized for speed, automation, and fine-grained control.

#### 🔧 Example Usage:
```bash
totalrecon.exe --only cpu,gpu,ram --export json,pdf --output "D:\Reports"
```

#### 🏁 Key CLI Options:
| Flag               | Function                                           |
| ------------------ | -------------------------------------------------- |
| `--full`           | Run a full scan (all modules)                      |
| `--only <modules>` | Run selected modules (comma-separated)             |
| `--export <types>` | Specify export formats: json, csv, html, pdf, etc. |
| `--output <path>`  | Set custom directory for reports and logs          |
| `--no-confirm`     | Disable interactive confirmations                  |
| `--quiet`          | Suppress output (silent mode)                      |
| `--help`           | Show help and usage guide                          |

### 🖼️ Graphical User Interface (GUI) (Planned)
A modern GUI is planned for release, using either WPF (C#) or Tkinter (Python). It will feature:

- 📂 Sidebar navigation for module selection
- ⏱️ Real-time progress indicators
- 🌗 Light/Dark theme toggle
- 📤 Export controls for all supported formats
- 🔐 Privilege level detection & status badge

All GUI interactions will reflect real CLI executions for transparency and reproducibility.

### 🛠️ Configuration File Support

For repeatable setups and bulk deployment, TotalRecon will support customizable configuration files:

# config.yaml
run_mode: full
export_formats:
  - json
  - html
output_dir: "D:/ReconReports/"
excluded_modules:
  - clipboard
  - shellbags

> Configuration files eliminate the need to retype common CLI flags and make bulk scanning more consistent.

### 📚 Built-in Help & Documentation

Help is always accessible via:
```bash
totalrecon.exe --help
```

---

> ⚡ Whether you're running deep diagnostics, monitoring performance, or performing forensic audits — TotalRecon adapts to your permission level, workflow, and preferences.
