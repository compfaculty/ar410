## HOWTO: Install and run activness-reporter

This document is for **end users** who just want to download a binary, configure
credentials, and run the tool. No Rust toolchain is required.

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

## 3. Configure environment (.env)

`activness-reporter` expects Activeness credentials as environment variables.
The easiest way to provide them is via a `.env` file in the same directory as
the binary.

Create a file named `.env` alongside the executable with contents like:

```env
ACTIVENESS_EMAIL=your@email
ACTIVENESS_PASSWORD=your_password
# Optional: override API URL (default: https://activeness.social/api)
# ACTIVENESS_API_URL=https://activeness.social/api
```

Notes:

- `ACTIVENESS_EMAIL` and `ACTIVENESS_PASSWORD` must match your Activeness
  account.
- You can use `ACTIVENESS_PSW` instead of `ACTIVENESS_PASSWORD` if configured
  that way in your environment.
- Leave `ACTIVENESS_API_URL` commented out unless you have a custom endpoint.

If you prefer, you can set these variables directly in your shell instead of
using `.env`.

---

## 4. First run

### Windows (PowerShell)

From the folder containing `activness-reporter.exe` and `.env`:

```powershell
.\activness-reporter.exe
```

This starts the TUI (text UI) for viewing and processing Activeness targets.

Other common commands:

- Headless mode (for schedulers / automation):

  ```powershell
  .\activness-reporter.exe --headless
  ```

- Refresh browser profiles / site logins:

  ```powershell
  .\activness-reporter.exe --update-profile
  ```

- Use local JSON targets file (skips Activeness API; useful for testing):

  ```powershell
  .\activness-reporter.exe --from-json .\targets.json
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
  - Verify `ACTIVENESS_EMAIL` and `ACTIVENESS_PASSWORD` are set and correct.

- **Authentication or API errors**
  - Confirm your Activeness account is active and credentials are valid.
  - If you are using a custom backend, set `ACTIVENESS_API_URL` accordingly.

- **Terminal display issues (TUI)**
  - Use a modern terminal emulator.
  - On Windows, prefer Windows Terminal or PowerShell over legacy `cmd.exe`.

- **Browser automation not working**
  - Make sure your environment allows outgoing HTTPS connections.
  - Some corporate security software may interfere with automated browsers.

If issues persist, capture the full console output and share it with whoever
manages your Activeness deployment.

