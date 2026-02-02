# 🔴 Red Team Lab

A **Next.js-powered** red team simulation platform for executing adversary attack emulations against Windows endpoints. Execute real-world TTPs from known threat actors to validate EDR detections and test your security controls.

---

## 📋 Table of Contents

- [Features](#-features)
- [Prerequisites](#-prerequisites)
- [Installation](#-installation)
- [Running the Application](#-running-the-application)
- [Test Scenarios](#-test-scenarios)
  - [Atomic Scenarios](#atomic-scenarios)
  - [Adversary Campaigns](#adversary-campaigns)
  - [Threat Actor Library](#threat-actor-library)
- [Usage Guide](#-usage-guide)
- [Project Structure](#-project-structure)
- [Troubleshooting](#-troubleshooting)

---

## ✨ Features

- **Atomic TTP Execution**: Run individual MITRE ATT&CK techniques with detailed output
- **Adversary Campaigns**: Multi-stage attack chains emulating real-world threat actors (APT28, APT1, Scattered Spider, etc.)
- **Threat Actor Library**: 10+ ransomware/APT groups with 45+ detection-triggering scripts
- **MITRE ATT&CK Mapping**: Every technique linked to official MITRE documentation
- **Revert Capabilities**: Undo system modifications with one-click revert scripts
- **Parameter Inputs**: Dynamic input fields for tester-specified targets (IPs, hostnames, URLs)

---

## 📦 Prerequisites

Before installing, ensure you have the following software installed on your system:

### Node.js

- **Required Version**: Node.js 18.x or later (LTS recommended)
- **Download**: [https://nodejs.org/](https://nodejs.org/)

**Verify Installation:**
```bash
node --version
# Expected output: v18.x.x or higher

npm --version  
# Expected output: 9.x.x or higher
```

### Target Environment

- **Operating System**: Windows 10/11 or Windows Server 2016+
- **PowerShell**: Version 5.1 or later (included with Windows)
- **Permissions**: Administrator privileges required for most TTPs
- **Network**: Connectivity to target hosts for lateral movement scenarios

---

## 🚀 Installation

### 1. Clone or Download the Repository

```bash
# If using Git
git clone <repository-url> red-team-lab
cd red-team-lab

# Or if you have the folder already
cd /path/to/RTL
```

### 2. Install Dependencies

Run the following command to install all required Node.js packages:

```bash
npm install
```

This will install:
- **Next.js 16.1.1** - React framework for the web application
- **React 19.2.3** - UI library
- **TypeScript** - Type-safe JavaScript
- **ESLint** - Code linting

### 3. Verify Installation

Ensure all dependencies are correctly installed:

```bash
npm ls
```

---

## ▶️ Running the Application

### Development Mode (Recommended)

Start the development server with hot-reloading:

```bash
npm run dev
```

**Output:**
```
▲ Next.js 16.1.1
- Local:        http://localhost:3000
- Environments: .env.local

✓ Ready in 2.3s
```

Open your browser and navigate to **[http://localhost:3000](http://localhost:3000)**

### Production Build

For production deployment:

```bash
# Build the application
npm run build

# Start the production server
npm start
```

### Available Scripts

| Command | Description |
|---------|-------------|
| `npm run dev` | Start development server with hot-reload |
| `npm run build` | Create optimized production build |
| `npm start` | Start production server |
| `npm run lint` | Run ESLint for code quality checks |

---

## 🧪 Test Scenarios

### Atomic Scenarios

Individual TTPs that can be executed independently. Access via the **Dashboard** at `http://localhost:3000`.

| Scenario | Adversary | MITRE ID | Difficulty |
|----------|-----------|----------|------------|
| Host Reconnaissance (PowerShell) | Red Team Ops | T1049, T1057 | Easy |
| Privilege Escalation Check | APT28 | T1134 | Medium |
| Lateral Movement to Domain Controller | APT28 | T1021.002 | Hard |
| C2 Connectivity Check | Scattered Spider | T1071 | Easy |
| Persistence (Registry) | APT1 | T1547.001 | Medium |
| Defense Evasion (Clear Logs) | Red Team Ops | T1070.001 | Medium |
| Credential Dumping (Active) | APT1 | T1003.001 | Hard |
| Initial Access (Payload Staging) | APT45 | T1105 | Easy |
| Exfiltration via DNS | APT45 | T1048.003 | Hard |

### Adversary Campaigns

Multi-stage attack chains accessible via **Adversary Campaigns** at `http://localhost:3000/campaigns`.

| Campaign | Adversary | Steps | Description |
|----------|-----------|-------|-------------|
| Full Killchain Emulation | Red Team Ops | 7 | Complete end-to-end simulation |
| Operation XAgent | APT28 | 4 | Recon → Priv Esc → Lateral → Cred Dump |
| Operation Comment Crew | APT1 | 3 | Persistence and credential harvesting |
| Cloud & Identity Siege | Scattered Spider | 4 | C2, evasion, and persistence |
| North Korean Info Stealer | APT45 | 3 | Rapid collection and credential theft |
| PlugX Propagation | Mustang Panda | 3 | Lateral movement and C2 beaconing |
| Conti/Ryuk Precursor | Wizard Spider | 4 | Ransomware attack prelude |

### Threat Actor Library

Detailed TTP libraries for 10+ threat actors, accessible via the **Threat Library** page:

| Threat Actor | Aliases | Notable TTPs |
|--------------|---------|--------------|
| **LockBit 3.0** | LockBit Black | WMI Shadow Copy Delete, Registry Mod, Inhibit Recovery |
| **Black Basta** | - | Phishing, EDR Disable, Priv Esc Exploits, RDP Lateral |
| **ALPHV/BlackCat** | Noberus | ProxyShell, PowerShell Execution, Scheduled Tasks |
| **AvosLocker** | - | Web Exploits, Shadow Delete, RAT Install, Encryption |
| **BianLian** | - | VM Detection, Packing, USB Spread, Encryption |
| **Cl0p** | TA505, FIN11 | MOVEit Exploit, Registry Persistence, Log Clear |
| **Conti** | Wizard Spider | Fast Encryption, Web Exfiltration |
| **DragonForce** | DragonForce Malaysia | Defender Disable, Self-Delete, Encryption |
| **SafePay** | - | RDP Scan, UAC Bypass, Credential Dump, FTP Exfil |
| **Generic Discovery** | Red Team Ops | Network Config, Groups, User, AD Enumeration |

---

## 📖 Usage Guide

### Executing an Atomic Scenario

1. Navigate to the **Dashboard** at `http://localhost:3000`
2. Select a scenario card (e.g., "Host Reconnaissance")
3. Review the MITRE technique details and estimated duration
4. Enter required parameters:
   - **Target IP**: The IP address of the target host
   - **C2 Server**: Your command & control server address
5. Click **EXECUTE SCENARIO**
6. Monitor the terminal output for results

### Running an Adversary Campaign

1. Navigate to **Adversary Campaigns** at `http://localhost:3000/campaigns`
2. Select a campaign (e.g., "Operation XAgent")
3. Review the attack chain steps
4. Click **INITIATE CAMPAIGN**
5. Enter the required target parameters:
   - **Target IP**: Primary target host
   - **C2 Server**: Callback server for exfiltration
6. The campaign will execute each step sequentially
7. Monitor output and observe EDR alerts

### Using the Threat Library

1. Navigate to the **Threat Library** page
2. Select a threat actor (e.g., "LockBit 3.0")
3. Browse available TTPs organized by MITRE tactic
4. Click **EXECUTE** on any TTP to run it
5. For TTPs with modifications, use **REVERT** to undo changes

### Reverting System Changes

Some TTPs modify system state (registry, services, etc.). To revert:

1. After executing a TTP, look for the **REVERT** button
2. Click **REVERT** to execute the corresponding `_revert.ps1` script
3. Verify the system returns to its original state

---

## 📁 Project Structure

```
RTL/
├── src/
│   ├── app/                    # Next.js App Router pages
│   │   ├── page.tsx           # Dashboard (Atomic Scenarios)
│   │   ├── campaigns/         # Adversary Campaigns pages
│   │   │   ├── page.tsx       # Campaign list
│   │   │   └── [id]/          # Individual campaign execution
│   │   ├── scenario/          # Scenario execution pages
│   │   └── api/               # API routes for script execution
│   ├── components/            # Reusable UI components
│   ├── lib/
│   │   └── types.ts           # TypeScript types, scenarios, campaigns
│   └── scenarios/             # PowerShell execution scripts
│       ├── *.ps1              # Root-level atomic scripts
│       ├── lockbit/           # LockBit threat actor scripts
│       ├── blackbasta/        # Black Basta scripts
│       ├── alphv/             # ALPHV/BlackCat scripts
│       ├── clop/              # Cl0p scripts
│       ├── dragonforce/       # DragonForce scripts
│       ├── safepay/           # SafePay scripts
│       ├── bianlian/          # BianLian scripts
│       ├── avoslocker/        # AvosLocker scripts
│       ├── conti/             # Conti scripts
│       └── library/           # Generic discovery modules
├── public/                     # Static assets
├── package.json               # Dependencies and scripts
├── tsconfig.json              # TypeScript configuration
└── next.config.ts             # Next.js configuration
```

---

## 🔧 Troubleshooting

### Common Issues

#### Port 3000 Already in Use

```bash
# Find the process using port 3000
lsof -i :3000

# Kill the process or use a different port
npm run dev -- -p 3001
```

#### Node.js Version Mismatch

```bash
# Check your Node version
node --version

# If using nvm, switch to the correct version
nvm use 18
```

#### npm Install Fails

```bash
# Clear npm cache and retry
npm cache clean --force
rm -rf node_modules package-lock.json
npm install
```

#### PowerShell Scripts Not Executing

1. Ensure you're running on a **Windows** target machine
2. Verify **PowerShell ExecutionPolicy** allows script execution:
   ```powershell
   Set-ExecutionPolicy -ExecutionPolicy Bypass -Scope Process
   ```
3. Run PowerShell as **Administrator** for privilege-required TTPs

#### Script Execution Errors

- **Access Denied**: Ensure Administrator privileges
- **Network Errors**: Verify target IP/hostname is reachable
- **LSASS Dump Fails**: Requires elevated privileges and may be blocked by EDR

---

## ⚠️ Disclaimer

This tool is designed for **authorized security testing only**. Ensure you have explicit written permission before executing any scenarios against systems you do not own. Misuse of this tool may violate computer fraud and abuse laws.

---

## 📝 License

[MIT License](LICENSE) - See LICENSE file for details.
