## HOWTO for non-technical folks (English)

*Ukrainian (ua): [HOWTO_FOR_NON_TECH_FOLKS.ua.md](HOWTO_FOR_NON_TECH_FOLKS.ua.md)*

This guide is a simple, click-by-click setup for everyday users.
You do not need Rust or any developer tools.

---

## 0) Create your Activeness account first

1. Open [activeness.social](https://activeness.social/).
2. Create your account (or sign in if you already have one).
3. You will use this same login in `.env`:
   - `ACTIVENESS_EMAIL` = your Activeness account email
   - `ACTIVENESS_PASSWORD` = your Activeness account password

Tip before automation:
- It is worth spending a few minutes on the website in a normal browser first,
  so you can see how the feed, stats, and targets work in general.

---

## 1) Quick start

### 1. Download the app archive

1. Open [Releases](https://github.com/compfaculty/ar410/releases).
2. Download the file for your system (Windows users: `.zip`).
3. Save it to `Downloads` (or another folder you use often).

![Step 1](docs/img/step1.png)

### 2. Unzip into a folder you can find later

1. Right-click the downloaded `.zip`.
2. Click **Extract All...**.
3. Open the extracted folder and make sure `activness-reporter.exe` exists.

![Step 2](docs/img/step2.png)

### 3. Create a `.env` file in the same folder as `activness-reporter.exe`

1. Open Notepad.
2. Paste this template:

```env
ACTIVENESS_EMAIL=your@email
ACTIVENESS_PASSWORD=your_password
# Optional:
# ACTIVENESS_API_URL=https://activeness.social/api
```

3. Replace email/password with your real account.

4. Save the file as `.env` in the same folder as `activness-reporter.exe`.
5. In Windows Save dialog, choose **Save as type: All files (*.*)** to avoid `.env.txt`.

![Step 10](docs/img/step10.png)
![Step 11](docs/img/step11.png)

### 4. Open terminal in that folder

![Step 4](docs/img/step4.png)

### 5. Run the app and initialize browser profiles

Run:

```powershell
.\activness-reporter.exe --update-profile
```

You can also check options with:

```powershell
.\activness-reporter.exe --help
```

![Step 6](docs/img/step6.png)
*Start the profile update / browser initialization flow.*

![Step 7](docs/img/step7.png)
*On the first run, the app may install browser components and open a browser window for login.*

![Step 8](docs/img/step8.png)
*Use it like a regular browser: log in, pass captchas if needed, and close tabs you do not need. This browser state is saved for automation.*

![Step 9](docs/img/step9.png)
*When done in the browser, return to the console and press Enter. It closes the browser (sometimes you may need to wait a bit or press Enter again).*

### 6. Start normal run

Run:

```powershell
.\activness-reporter.exe
```

![Step 12](docs/img/step12.png)
*This is what you should see in a normal run.*

If everything looks good, you can quit (press `q`) and run again with headless mode:

```powershell
.\activness-reporter.exe --headless
```

This hides the browser window and runs in the background.

If something goes wrong, quit and start again first.

![Running app](docs/img/running-ar410.jpg)
*Expected running state of `activness-reporter` (final result).*
---

