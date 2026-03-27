## HOWTO: Install and run activness-reporter

*Українська (ua): [HOWTO.ua.md](HOWTO.ua.md)*

This document is for **end users** who just want to download a binary, configure
credentials, and run the tool. No Rust toolchain is required.

---

## 0. Create your Activeness account first

Before downloading anything:

1. Open [activeness.social](https://activeness.social/).
2. Create an account (or sign in if you already have one).
3. Keep this login ready for configuration:
   - `ACTIVENESS_EMAIL` = your Activeness account email
   - `ACTIVENESS_PASSWORD` = your Activeness account password

Recommended before automation:
- Spend a few minutes using the site manually in your browser (open feed, stats,
  and target pages) so you can understand how the workflow looks and feels.

---

## 1. Download the binary

1. Go to the [Releases](https://github.com/compfaculty/ar410/releases) page.
2. Pick the latest version (for example, `v0.1.0`).
3. Download the archive for your operating system:
   - **Windows**: `activness-reporter-x86_64-pc-windows-msvc.zip`
   - **Linux**: `activness-reporter-x86_64-unknown-linux-gnu.tar.gz`
   - **macOS (Intel)**: `activness-reporter-x86_64-apple-darwin.tar.gz`
   - **macOS (Apple Silicon)**: `activness-reporter-aarch64-apple-darwin.tar.gz`

4. Save the file to a directory of your choice (for example, `Downloads/`).

---

## 2. Unpack the archive

### Windows

1. Right‑click the downloaded `.zip` file and choose **Extract All…**, or use PowerShell:

   ```powershell
   Expand-Archive -Path .\activness-reporter-x86_64-pc-windows-msvc.zip -DestinationPath .\activness-reporter
   cd .\activness-reporter
   ```

2. You should see `activness-reporter.exe` in the extracted folder.

### Linux / macOS

From a terminal:

```bash
mkdir -p activness-reporter
tar -xzf activness-reporter-*.tar.gz -C activness-reporter
cd activness-reporter
```

You should see an executable named `activness-reporter`.

On some systems you may need to mark it as executable:

```bash
chmod +x activness-reporter
```

---

## 3. Configure environment (credentials)

`activness-reporter` expects Activeness credentials as **environment variables**.
Start with **Method 1** (`.env` file); the other methods are optional.

Example values to put in `.env` or set by hand:

```env
ACTIVENESS_EMAIL=your@email
ACTIVENESS_PASSWORD=your_password
# Optional: override API URL (default: https://activeness.social/api)
# ACTIVENESS_API_URL=https://activeness.social/api
```

### Method 1 — `.env` file (recommended)

Do this if you are on Windows and are not comfortable with the terminal yet.

1. Open **Notepad** (or another **plain text** editor — not Microsoft Word).
2. Paste the three lines above. Replace `your@email` with your Activeness email
   and `your_password` with your password. Leave the `#` lines as they are
   unless you need a custom API URL.
3. Choose **File → Save As…**
4. In the file dialog, open the **same folder** that contains
   `activness-reporter.exe` (Windows) or `activness-reporter` (Linux/macOS).
5. In **File name**, type exactly: `.env` (a dot, then the letters env).
6. In **Save as type** (Windows), choose **All files (`*.*`)** so Windows does
   not rename the file to `.env.txt`.

**Tip (Windows):** In File Explorer, use **View → Show → File name extensions**
so you can see if the file was accidentally saved as `env.txt` instead of
`.env`.

### Method 2 — only for the current terminal session

Use this if you cannot create a `.env` file. **Closing the terminal removes
these values.** For everyday use, Method 1 is easier.

1. Open a terminal in the program folder (see [section 4](#4-first-run)).

**PowerShell** (prompt often starts with `PS`):

```powershell
$env:ACTIVENESS_EMAIL = "your@email"
$env:ACTIVENESS_PASSWORD = "your_password"
```

**Command Prompt (CMD)** (classic black window; no `PS` in the prompt):

```bat
set ACTIVENESS_EMAIL=your@email
set ACTIVENESS_PASSWORD=your_password
```

In CMD, do **not** put spaces around the `=` sign.

### Method 3 — Windows “Environment variables” (advanced)

This stores credentials for **your user account** (or for the whole PC if you
use *system* variables). Use it only if you understand that the values are kept
in Windows settings until you remove them.

1. Open **Settings → System → About → Advanced system settings**
   (or search Windows for “environment variables”).
2. Click **Environment variables…**
3. Under **User variables** click **New…** and add `ACTIVENESS_EMAIL`, then
   repeat for `ACTIVENESS_PASSWORD`. *(System variables apply to all users and
   usually need administrator rights; prefer user variables for personal
   logins.)*
4. **Close every open terminal window**, then open a **new** one so the
   program sees the new values.

### Notes

- `ACTIVENESS_EMAIL` and `ACTIVENESS_PASSWORD` must match your Activeness
  account.
- You can use `ACTIVENESS_PSW` instead of `ACTIVENESS_PASSWORD` if that is how
  your environment is set up.
- Leave `ACTIVENESS_API_URL` commented out unless you have a custom endpoint.

---

## 4. First run

### Windows

Follow the steps in order the first time.

#### Step 1 — Open a terminal in the program folder

Pick **one** approach.

**Easiest (File Explorer):**

1. Open the folder that contains **`activness-reporter.exe`** and your **`.env`**
   file.
2. Click once in the **address bar** (where the path is shown).
3. Type `powershell` and press **Enter** to open PowerShell in that folder,
   **or** type `cmd` and press **Enter** to open Command Prompt.

**Manual:**

1. Open **Windows Terminal**, **Windows PowerShell**, **PowerShell 7**, or
   **Command Prompt**.
2. Go to the folder with `cd`, for example:

   ```powershell
   cd D:\Downloads\activness-reporter
   ```

   If you use **CMD** and the program is on another drive (for example `D:`),
   use:

   ```bat
   cd /d D:\Downloads\activness-reporter
   ```

#### Step 2 — Know which shell you are using

- **Windows Terminal** is only the window: each **tab** is still either
  PowerShell or CMD — use the matching commands below.
- **PowerShell:** the prompt usually shows **`PS`**. You **must** type
  **`.\`** before the program name (security feature).
- **CMD:** the prompt looks like `C:\...>`. You can run the `.exe` name **without**
  **`.\`**.

#### Quick reference

| You opened… | Run the program like this |
|-------------|---------------------------|
| PowerShell (in the program folder) | `.\activness-reporter.exe` |
| CMD (in the program folder) | `activness-reporter.exe` |
| Linux / macOS (in the program folder) | `./activness-reporter` |

#### Step 3 — Start the TUI (default)

**PowerShell:**

```powershell
.\activness-reporter.exe
```

**Command Prompt (CMD):**

```bat
activness-reporter.exe
```

This starts the TUI (text UI) for viewing and processing Activeness targets.

#### Other common commands

**Headless mode** (for schedulers / automation):

```powershell
.\activness-reporter.exe --headless
```

```bat
activness-reporter.exe --headless
```

**Refresh browser profiles / site logins:**

```powershell
.\activness-reporter.exe --update-profile
```

```bat
activness-reporter.exe --update-profile
```

**Local JSON targets file** (skips Activeness API; useful for testing):

```powershell
.\activness-reporter.exe --from-json .\targets.json
```

```bat
activness-reporter.exe --from-json targets.json
```

### Linux / macOS

From the folder containing `activness-reporter` and `.env`:

```bash
./activness-reporter
```

Headless mode:

```bash
./activness-reporter --headless
```

Refresh profiles:

```bash
./activness-reporter --update-profile
```

Run with a local JSON file:

```bash
./activness-reporter --from-json targets.json
```

---

## 5. Playwright first‑run behavior

The tool uses a browser automation engine under the hood (via Playwright). On
first run it may:

- Download browser binaries
- Prepare browser profiles on disk

This can take extra time and disk space the first time you run it. Subsequent
runs are faster.

If you see longer startup times on the first run, this is expected.

---

## 6. Troubleshooting

- **Nothing happens / exits immediately**
  - Check that `.env` is present in the same directory as the binary.
  - On Windows, make sure the file is named `.env`, not `.env.txt` or `env.txt`
    (turn on file name extensions in Explorer).
  - Verify `ACTIVENESS_EMAIL` and `ACTIVENESS_PASSWORD` are set and correct.

- **`activness-reporter` / command not found (PowerShell on Windows)**
  - In **PowerShell**, run `.\activness-reporter.exe` from the folder that
    contains the `.exe`, including the `.\` at the start.

- **Authentication or API errors**
  - Confirm your Activeness account is active and credentials are valid.
  - If you are using a custom backend, set `ACTIVENESS_API_URL` accordingly.

- **Terminal display issues (TUI)**
  - Use a modern terminal emulator.
  - On Windows, prefer Windows Terminal or PowerShell over legacy `cmd.exe`
    for the best compatibility.

- **Browser automation not working**
  - Make sure your environment allows outgoing HTTPS connections.
  - Some corporate security software may interfere with automated browsers.

If issues persist, capture the full console output and share it with whoever
manages your Activeness deployment.
