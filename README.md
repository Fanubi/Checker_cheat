# STM 3.0 — System Tools Menu / Tools Launcher

> Created by **fanubi** · Discord: `@fanubi`

STM 3.0 is a Windows desktop launcher that bundles a curated set of forensic and system analysis utilities into a single portable `.exe`. No installation required — everything is embedded inside the binary and extracted to a temporary folder at runtime, cleaned up automatically on exit.

---

## Features

### 🔍 NirSoft Utilities (embedded)
All tools launch directly from the binary — no external files needed.

| Tool | Description |
|---|---|
| **LastActivityView** | Shows recent user activity — opened files, programs, network connections |
| **UserAssistView** | Reads Windows UserAssist registry — programs launched via Explorer |
| **USBDeview** | Full history of all USB devices ever connected to the system |
| **ExecutedProgramsList** | List of all programs that have ever been executed |
| **FolderChangesView** | Monitors and logs real-time folder changes |
| **JumpListsView** | Reads Windows Jump Lists — recently opened files per application |
| **MUICacheView** | Shows programs registered in the MUI Cache registry key |
| **OpenSaveFilesView** | History of all files opened or saved via Open/Save dialogs |
| **RecentFilesView** | Recently accessed files from the shell |
| **ShellBagsView** | Reads ShellBags — every folder ever browsed, even deleted ones |
| **InjectedDLL** | Lists all DLLs currently injected into running processes |
| **BrowserDownloadsView** | History of all browser downloads across Chrome, Firefox, Edge |

### 🔎 Other Tools (embedded)
- **Everything** — instant file search across the entire drive
- **ShellBag Analyzer & Cleaner** — deep ShellBag forensic analysis

### ⚙️ STM 2.0 — System Tools Menu (built-in, no batch file)
A fully integrated system toolkit running natively inside the launcher:
- **Open System Folders** — AppData, Prefetch, Temp, Recent Files, Registry Editor
- **System Information** — full `systeminfo` output rendered inside the app
- **TPM Management** — opens `tpm.msc`
- **Steam Accounts** — locates and opens `loginusers.vdf`
- **CrashDumps Folder** — opens `%LOCALAPPDATA%\CrashDumps`
- **Open Forums** — quick links to oplata.info and funpay.com
- **Open Mail Services** — mail.ru, Gmail, Yandex Mail

---

## 🗑️ Deletion / Cleanup Check
Automated forensic scan that detects signs of deliberate system cleanup. Each check contributes to a total **suspicion score** with an automatic verdict.

### Checks performed

| Tab | What it looks for |
|---|---|
| **Recycle Bin** | Suspicious filenames (cheats, injectors, cleaners) |
| **Prefetch** | Cleaner tools and cheat software in launch history — survives uninstall |
| **Recent Files** | Suspicious filenames, abnormal time gaps in history |
| **ShellBags** | Missing `MRUListEx` (bags were cleared), empty bag registry |
| **USN Journal** | Abnormally low First USN (journal wiped/recreated), shadow copy status |
| **Event Log** | Event ID 1102 (Security log cleared), Event ID 104 (System log cleared), Defender status |
| **Cleaners** | Installed or previously run: CCleaner, BleachBit, Privazer, Eraser, Glary Utilities, Wise Cleaner, Privacy Eraser, MRU-Blaster, HardWipe |
| **Registry** | Run dialog history, Explorer typed paths, UserAssist decoded entries (ROT13) |
| **Thumbnails** | Missing or suspiciously small thumbnail cache |

### Verdict system
| Score | Verdict |
|---|---|
| 0 | ✅ Clean |
| 1–4 | 🟡 Low suspicion |
| 5–9 | ⚠ Suspicious |
| 10–14 | 🚨 Highly suspicious |
| 15+ | 🚫 Almost certainly cleaned |

Each finding is listed with a weight bar `[█████]` and a description so you can see exactly what triggered the score.

---

## 🖥️ Viewer modes
Every NirSoft tool has two launch options:
- **VIEW** — runs the tool with `/stext` output parsed and displayed inside the launcher in a styled text panel
- **EXT** — opens the tool in its own native window

---

## Technical details
- Built with **Python 3 + tkinter** — no third-party UI dependencies
- All utilities are **base64-encoded and embedded** inside the script, extracted to `%TEMP%\stm3_*` at runtime and deleted on exit
- Single-file build via **PyInstaller** (`--onefile --noconsole`)
- Runs on **Windows 10 / 11**

---

The resulting `.exe` is fully self-contained — no external files or folders required.

---

## License
Personal use only. Not for redistribution.
