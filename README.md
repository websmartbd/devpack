<div align="center">

<img src="https://img.shields.io/badge/DevPack-PHP%20Hosting%20Panel-3258E8?style=for-the-badge&logo=php&logoColor=white" alt="DevPack">

# DevPack

**Easy PHP Hosting with Subdomains & MySQL — All from your browser.**

[![PHP](https://img.shields.io/badge/PHP-8.0%2B-777BB4?style=flat-square&logo=php&logoColor=white)](https://php.net)
[![Apache](https://img.shields.io/badge/Apache-2.4%2B-D22128?style=flat-square&logo=apache&logoColor=white)](https://httpd.apache.org)
[![MySQL](https://img.shields.io/badge/MySQL-5.7%2B-4479A1?style=flat-square&logo=mysql&logoColor=white)](https://mysql.com)
[![License](https://img.shields.io/badge/License-MIT-22C55E?style=flat-square)](LICENSE)
[![Issues](https://img.shields.io/github/issues/websmartbd/devpack?style=flat-square&color=EF4444)](https://github.com/websmartbd/devpack/issues)
[![Stars](https://img.shields.io/github/stars/websmartbd/devpack?style=flat-square&color=F59E0B)](https://github.com/websmartbd/devpack/stargazers)

[🚀 Features](#-features) • [📦 Installation](#-installation) • [⚙️ Configuration](#%EF%B8%8F-configuration) • [🖥️ Usage](#%EF%B8%8F-usage) • [🔒 Security](#-security) • [🤝 Contributing](#-contributing) • [🐛 Bug Report](#-bug-report)

---

</div>

## 🌟 What is DevPack?

DevPack is a **self-hosted PHP hosting control panel** that allows you to easily:

- ✅ Create and manage custom **subdomains**
- ✅ Provision **MySQL databases** with a single click
- ✅ Upload and edit code directly from your browser using the **file manager**
- ✅ Monitor all your sites via a live **dashboard**
- ✅ Run perfectly on **Shared hosting (cPanel)**, **VPS**, or **Localhost**

> 💡 The easiest way to deploy PHP sites on your own server without needing deep technical knowledge.

---

## 🚀 Features

### 🌐 Subdomain Management
- Create a new subdomain simply by filling out a form
- Each subdomain resides in its own isolated directory
- Delete subdomains anytime with one click

### 🗄️ MySQL Database
- Provision dedicated databases for your subdomains
- Auto-generated database usernames and passwords
- Credentials securely stored in the `data/` folder
- Supports both cPanel API and VPS direct MySQL connections

### 📁 File Manager
- **Upload** — Drag & drop file uploading
- **Edit** — Built-in browser-based code editor
- **Manage** — Rename, Move, Delete, and create directories
- **Download** — Download any file instantly

### 📊 Live Dashboard
- Total subdomains count
- Total files deployed
- Storage used (Auto-formats to KB/MB/GB)
- Per-site file and folder listing

### 🛡️ Security
- CSRF protection across all forms
- Rate limiting for login attempts
- Session hardening (httpOnly, SameSite, Secure)
- Security headers (HSTS, CSP, X-Frame-Options, etc.)
- Dangerous PHP functions automatically disabled
- Sensitive directories protected via `.htaccess`

### ⚡ Server Support
| Type | Description |
|------|-------------|
| `local` | XAMPP / Laragon / WAMP / localhost |
| `cpanel` | Shared hosting with cPanel API |
| `vps` | Bare VPS / dedicated server |

---

## 📦 Installation

### Requirements

- PHP **8.0+**
- Apache with **mod_rewrite** enabled
- MySQL / MariaDB **5.7+**
- `AllowOverride All` enabled in your Apache configuration

### Step 1 — Clone the repository

```bash
git clone https://github.com/websmartbd/devpack.git
cd devpack
```

### Step 2 — Configure

Edit the `config/config.php` file with your details:

```php
// MySQL connection
define('DB_HOST', 'localhost');
define('DB_USER', 'root');
define('DB_PASS', '');

// Panel login
define('PANEL_PASS', 'your_secure_password_here');

// Hosting details
define('SERVER_TYPE', 'local'); // 'local', 'cpanel', or 'vps'
define('MAIN_DOMAIN', 'localhost'); // Your main domain name
```

### Step 3 — Secure Directory Permissions

Ensure that the `data/` and `sites/` directories are writable by the web server:

```bash
chmod -R 775 data sites
chown -R www-data:www-data data sites
```
*(On cPanel/Shared hosting, standard 755 permissions usually work fine).*

### Step 4 — Apache Virtual Host

```apache
<VirtualHost *:80>
    ServerName yourdomain.com
    ServerAlias *.yourdomain.com
    DocumentRoot /path/to/devpack
    DirectoryIndex index.php

    <Directory /path/to/devpack>
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
```

### Step 5 — Done! 🎉

Open `http://yourdomain.com` in your browser and log into the Control Panel!

---

## ⚙️ Configuration

### `config/config.php` — Core Settings

| Constant | Description | Default |
|----------|-------------|---------|
| `DB_HOST` | MySQL host | `localhost` |
| `DB_USER` | MySQL root/admin username | — |
| `DB_PASS` | MySQL password | — |
| `DB_PORT` | MySQL port | `3306` |
| `PANEL_PASS` | Control panel login password | — |
| `MAIN_DOMAIN` | Your main domain | `localhost` |
| `SERVER_TYPE` | Hosting type | `local` |
| `SITES_ROOT` | Path where sites are stored | `./sites` |
| `DATA_DIR` | Path for credentials & logs | `./data` |
| `DB_PREFIX_SEP` | DB name separator | `_` |

### Server Types

**`local`** — XAMPP/Laragon/WAMP:
```php
define('SERVER_TYPE', 'local');
define('MAIN_DOMAIN', 'localhost');
```

**`cpanel`** — Shared hosting:
```php
define('SERVER_TYPE', 'cpanel');
define('MAIN_DOMAIN', 'yourdomain.com');
// cPanel API credentials also needed in config
```

**`vps`** — Bare VPS:
```php
define('SERVER_TYPE', 'vps');
define('MAIN_DOMAIN', 'yourdomain.com');
```

---

## 🖥️ Usage

### Control Panel

1. Visit `https://yourdomain.com/` (or wherever DevPack is hosted)
2. Log in using your `PANEL_PASS`
3. Manage everything directly from the Dashboard

### Steps to Deploy a New Site

```text
1. Click "Create Subdomain" → Enter subdomain name (e.g., myapp)
   → myapp.yourdomain.com is instantly created!

2. Go to "File Manager" → Upload or edit your code directly in the browser.

3. (Optional) Click "Create Database" → Provision a MySQL DB.
   → Credentials will automatically be saved and displayed.

4. Done! myapp.yourdomain.com is now live!
```

### File Structure

```text
devpack/
├── index.html             # Landing page (static HTML)
├── index.php              # Login page + Main router
├── control-panel.php      # Admin dashboard
├── file-manager.php       # File manager functionality
├── sqldb.php              # Database manager functionality
├── .htaccess              # Apache rules & security
│
├── config/
│   ├── config.php         # ⚙️  Main configuration
│   ├── router.php         # Subdomain routing logic
│   ├── security.php       # Security helpers (CSRF, rate limit)
│   ├── api.php            # Internal API handlers
│   └── monitor.php        # System monitoring
│
├── sites/                 # 📁 All subdomain files stored here
│   └── myapp/             #    → myapp.yourdomain.com
│       └── index.php
│
└── data/                  # 🔒 Sensitive data (not web-accessible)
    ├── .credentials/      #    DB credentials per subdomain
    └── .rate_limits.json  #    Login rate limit data
```

---

## 🔒 Security

DevPack takes security seriously:

| Feature | Details |
|---------|---------|
| **CSRF Protection** | Token validation on all POST requests |
| **Rate Limiting** | 5 login attempts per 5 minutes (configurable) |
| **Session Security** | httpOnly, SameSite=Strict, Secure cookies |
| **HSTS** | Enforces HTTPS in production (31536000s) |
| **CSP** | Strict Content-Security-Policy headers |
| **X-Frame-Options** | Protects against Clickjacking |
| **Directory Protection** | `data/` and `config/` are blocked via `.htaccess` |
| **PHP Hardening** | Dangerous functions like `exec`, `shell_exec` are disabled |

> ⚠️ **Important:** In production, ensure `PANEL_PASS` is strong and set the `config/config.php` file permissions to `644`.

---

## 🤝 Contributing

DevPack is an open-source project. Contributions are highly appreciated!

### How to Contribute

```bash
# 1. Fork the repo on GitHub

# 2. Clone your fork locally
git clone https://github.com/YOUR_USERNAME/devpack.git
cd devpack

# 3. Create a new branch
git checkout -b feature/your-feature-name
# Or for a bug fix:
git checkout -b fix/issue-description

# 4. Make your changes and commit
git add .
git commit -m "feat: add your feature description"

# 5. Push to your fork
git push origin feature/your-feature-name

# 6. Open a Pull Request on the main repository!
```

### Commit Message Format

```text
feat: Added a new feature
fix: Fixed a bug
docs: Updated documentation
style: Code formatting (no logic changes)
refactor: Code restructuring
test: Added or updated tests
chore: Build processes, configuration updates
```

### Contribution Ideas

- [ ] Nginx support
- [ ] PHP version selector per subdomain
- [ ] Automatic SSL via Let's Encrypt
- [ ] Backup & restore functionality
- [ ] Two-factor authentication
- [ ] Site-level analytics
- [ ] Docker support
- [ ] Multi-admin user system
- [ ] Email notification system
- [ ] Subdomain traffic monitoring

### Code Guidelines

- Ensure compatibility with PHP 8.0+
- Always perform input validation on security-sensitive functions
- Update the README if adding new features
- Both English and Bengali comments are acceptable in the codebase

---

## 🐛 Bug Report

If you discover a bug or run into issues, please report it via **[GitHub Issues](https://github.com/websmartbd/devpack/issues)**.

### Before Reporting a Bug

1. Search existing issues to avoid duplicates.
2. Check if you are using the latest version.
3. Verify your `config/config.php` settings.

### What to Include in Your Bug Report

```markdown
**Bug Description:**
[Clearly describe what the issue is]

**Steps to Reproduce:**
1. I did this...
2. Then I did this...
3. The error occurred

**Expected Behavior:**
[What you expected to happen]

**Actual Behavior:**
[What actually happened]

**Environment:**
- OS: [e.g., Ubuntu 22.04]
- PHP: [e.g., 8.2]
- Apache: [e.g., 2.4.54]
- MySQL: [e.g., 8.0]
- SERVER_TYPE: [local/cpanel/vps]
- Browser: [e.g., Chrome 120]

**Error Log (if any):**
[Paste the content of data/.error_log if applicable]
```

**[🐛 Report a Bug](https://github.com/websmartbd/devpack/issues/new?labels=bug&template=bug_report.md)**
&nbsp;&nbsp;
**[💡 Request a Feature](https://github.com/websmartbd/devpack/issues/new?labels=enhancement&template=feature_request.md)**

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).

```text
MIT License — You are free to use, modify, and distribute this software.
Attribution is appreciated but not required.
```

---

## 🙏 Acknowledgements

- [Tailwind CSS](https://tailwindcss.com) — UI styling
- [Remix Icon](https://remixicon.com) — Icons
- [JetBrains Mono](https://www.jetbrains.com/lp/mono/) — Monospace font
- [Inter](https://rsms.me/inter/) & [Plus Jakarta Sans](https://fonts.google.com/specimen/Plus+Jakarta+Sans) — Typography

---

<div align="center">

Made with ❤️ by [B.M Shifat](https://facebook.com/bmshifat0) & [websmartbd](https://github.com/websmartbd)

⭐ **Star the repo if you found it helpful!** ⭐

</div>
