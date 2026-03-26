## Activeness Reporter binaries

`activness-reporter` is a Rust CLI/TUI tool that talks to the Activeness service and automates reporting / engagement flows for multiple platforms (TikTok, YouTube, X/Twitter, Instagram, Facebook, Reddit).

This repository **only** hosts:

- Prebuilt binaries for Windows, Linux, and macOS
- End‑user documentation (HOWTO and changelog)

The source code lives in a private repository and is **not** published here.

---

## Download

- **Stable releases**: download the latest binary for your OS from the
  [Releases](https://github.com/compfaculty/ar410/releases) page.

Each release contains archives like:

- `activness-reporter-x86_64-pc-windows-msvc.zip`
- `activness-reporter-x86_64-unknown-linux-gnu.tar.gz`
- `activness-reporter-x86_64-apple-darwin.tar.gz`
- `activness-reporter-aarch64-apple-darwin.tar.gz`

Pick the archive matching your OS/architecture and follow the steps in
[HOWTO.md](HOWTO.md) (Українською: [HOWTO.uk.md](HOWTO.uk.md)).

---

## Quick usage

Once you have downloaded and unpacked the binary:

- **Run TUI (default)**:

  ```powershell
  ./activness-reporter
  ```

- **Headless mode for schedulers/automation**:

  ```powershell
  ./activness-reporter --headless
  ```

- **Refresh browser profiles / logins**:

  ```powershell
  ./activness-reporter --update-profile
  ```

- **Debug with local targets JSON** (skips Activeness API):

  ```powershell
  ./activness-reporter --from-json targets.json
  ```

For full step‑by‑step instructions, see [HOWTO.md](HOWTO.md) or
[HOWTO.uk.md](HOWTO.uk.md) (Ukrainian).

---

## Environment configuration

`activness-reporter` reads configuration from environment variables. The
recommended approach is to create a `.env` file next to the binary and let the
tool load it automatically.

Minimal example:

```env
ACTIVENESS_EMAIL=your@email
ACTIVENESS_PASSWORD=your_password
# Optional: override API URL (default: https://activeness.social/api)
# ACTIVENESS_API_URL=https://activeness.social/api
```

Environment variables:

| Variable             | Required | Description                                              |
|----------------------|----------|----------------------------------------------------------|
| `ACTIVENESS_EMAIL`   | Yes      | Activeness account email                                 |
| `ACTIVENESS_PASSWORD`| Yes      | Activeness account password (or `ACTIVENESS_PSW`)       |
| `ACTIVENESS_API_URL` | No       | Custom API endpoint (defaults to `https://activeness.social/api`) |

See [HOWTO.md](HOWTO.md) or [HOWTO.uk.md](HOWTO.uk.md) for OS‑specific details.

---

## Platforms

High‑level behavior:

- Authenticates to the Activeness API and fetches “targets”
- Classifies links into platforms (TikTok, YouTube, X/Twitter, Instagram, Facebook, Reddit)
- Performs platform‑specific reporting / engagement flows via an automated browser
- Updates target status back in Activeness and shows progress in the TUI

Details of the automation flows are implementation‑specific and may change
between releases.

---

## Changelog

See [CHANGELOG.md](CHANGELOG.md) for user‑visible changes between versions.

---

## License

This binary is distributed under the MIT License. See [LICENSE](LICENSE).

