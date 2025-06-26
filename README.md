# YouTube Cookie Refresher Workflow

This repository contains a GitHub Actions workflow designed to automatically refresh YouTube cookies by simulating browser activity using Playwright.

## 🔄 How It Works

1. **Clones** the `ytdownloader_backend` repository.
2. **Decrypts** the `cookies.enc` file using a secret key stored in GitHub Secrets.
3. **Uses Playwright** to:
   - Launch a virtual browser session
   - Inject cookies to authenticate with YouTube
   - Simulate activity (e.g., scrolling, interactions) to keep the session alive
4. **Encrypts** the updated cookies.
5. **Pushes** the refreshed `cookies.enc` back to the `ytdownloader_backend` repository.

## ✅ Purpose

YouTube cookies can expire or become invalid over time if unused. This workflow ensures they remain valid by simulating regular, human-like browser usage.

## 🔐 Security

- `COOKIE_KEY`: Used to encrypt and decrypt the cookie file.
- `PERSONAL_ACCESS_TOKEN`: GitHub token used to clone and push to the target repo securely.

Both secrets must be configured in the repository’s settings.

## 🕒 Schedule

The workflow can be triggered:
- **Automatically** via a daily cron job (e.g., `0 6 * * *` for 6 AM UTC)
- **Manually** by pushing changes to the `main` branch

## 📁 File Structure

- `cookies.enc`: Encrypted cookie file fetched from the `ytdownloader_backend` repo
- `spoof.py`: Python script using Playwright to simulate browsing
- `.github/workflows/...`: Contains the GitHub Actions YAML file automating the process

## 🛠 Requirements

Make sure the following Python packages are defined if you run this manually:
```bash
pip install playwright
playwright install
sudo apt install xvfb
