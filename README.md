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

DevPack একটি **self-hosted PHP hosting control panel** যা দিয়ে আপনি সহজেই:

- ✅ Custom **subdomain** তৈরি ও manage করতে পারবেন
- ✅ **MySQL database** provision করতে পারবেন এক ক্লিকে
- ✅ Browser থেকেই **file manager** দিয়ে code upload ও edit করতে পারবেন
- ✅ Live **dashboard** দিয়ে সব site monitor করতে পারবেন
- ✅ **Shared hosting (cPanel)**, **VPS**, বা **Localhost** — সব জায়গায় কাজ করে

> 💡 Technical knowledge ছাড়াই নিজের server-এ PHP site deploy করার সবচেয়ে সহজ উপায়।

---

## 🚀 Features

### 🌐 Subdomain Management
- একটি form fill করেই নতুন subdomain তৈরি করুন
- প্রতিটি subdomain আলাদা isolated directory-তে থাকে
- যেকোনো সময় subdomain delete করা যায়

### 🗄️ MySQL Database
- Subdomain-এর জন্য dedicated database তৈরি করুন
- Database username ও password auto-generate হয়
- Credentials সুরক্ষিতভাবে `data/` folder-এ store হয়
- cPanel API, VPS direct MySQL — উভয় সমর্থিত

### 📁 File Manager
- **Upload** — drag & drop file upload
- **Edit** — browser-based code editor
- **Rename / Move / Delete** — সব ফাইল operation
- **Create folder** — directory structure manage করুন
- **Download** — যেকোনো ফাইল download করুন

### 📊 Live Dashboard
- Total subdomains count
- Total files deployed
- Storage used (KB/MB/GB auto format)
- Per-site file listing

### 🛡️ Security
- CSRF protection সব forms-এ
- Rate limiting (login attempts)
- Session hardening (httpOnly, SameSite, Secure)
- Security headers (HSTS, CSP, X-Frame-Options, etc.)
- Dangerous PHP functions disabled
- `.htaccess` দিয়ে sensitive directories protected

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
- `AllowOverride All` in Apache config

### Step 1 — Clone the repository

```bash
git clone https://github.com/websmartbd/devpack.git
cd devpack
```

### Step 2 — Configure

`config/config.php` ফাইলটি edit করুন:

```php
// MySQL connection
define('DB_HOST', 'localhost');
define('DB_USER', 'your_db_user');
define('DB_PASS', 'your_db_password');
define('DB_PORT', 3306);

// Panel login password
define('PANEL_PASS', 'your_strong_password');

// Your domain
define('MAIN_DOMAIN', 'yourdomain.com');

// Server type: 'local', 'cpanel', or 'vps'
define('SERVER_TYPE', 'local');
```

### Step 3 — Set permissions

```bash
chmod 755 sites/
chmod 755 data/
chmod 644 config/config.php
```

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

Browser-এ `http://yourdomain.com` open করুন এবং Control Panel-এ login করুন।

---

## ⚙️ Configuration

### `config/config.php` — সব settings এখানে

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

1. `https://yourdomain.com/control-panel.php` এ যান
2. Password দিয়ে login করুন
3. Dashboard থেকে সব manage করুন

### নতুন Site Deploy করার ধাপ

```
1. "Create Subdomain" → subdomain name দিন (e.g., myapp)
   → myapp.yourdomain.com তৈরি হবে

2. "File Manager" → files upload করুন বা সরাসরি edit করুন

3. (Optional) "Create Database" → MySQL DB provision করুন
   → Credentials auto-save হবে

4. Done! myapp.yourdomain.com এ site live!
```

### File Structure

```
devpack/
├── index.php              # Landing page + main router
├── control-panel.php      # Admin dashboard
├── login.php              # Authentication
├── file-manager.php       # File manager
├── sqldb.php              # Database manager
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

DevPack নিরাপত্তার বিষয়ে গুরুত্বের সাথে কাজ করে:

| Feature | Details |
|---------|---------|
| **CSRF Protection** | সব POST forms-এ token validation |
| **Rate Limiting** | 5 attempts per 5 minutes (configurable) |
| **Session Security** | httpOnly, SameSite=Strict, Secure cookies |
| **HSTS** | Production-এ HTTPS enforce (31536000s) |
| **CSP** | Strict Content-Security-Policy headers |
| **X-Frame-Options** | Clickjacking protection |
| **Directory Protection** | `data/` ও `config/` web-inaccessible |
| **PHP Hardening** | `exec`, `shell_exec` etc. disabled |

> ⚠️ **Important:** Production-এ `PANEL_PASS` অবশ্যই strong password দিন এবং `config/config.php` file permission `644` রাখুন।

---

## 🤝 Contributing

DevPack একটি open-source project। আপনার contribution আমাদের কাছে অনেক গুরুত্বপূর্ণ!

### কীভাবে Contribute করবেন

```bash
# 1. Repo fork করুন
# (GitHub-এ "Fork" button click করুন)

# 2. Clone করুন
git clone https://github.com/YOUR_USERNAME/devpack.git
cd devpack

# 3. নতুন branch তৈরি করুন
git checkout -b feature/your-feature-name
# অথবা bug fix-এর জন্য:
git checkout -b fix/issue-description

# 4. Changes করুন এবং commit করুন
git add .
git commit -m "feat: add your feature description"

# 5. Push করুন
git push origin feature/your-feature-name

# 6. Pull Request খুলুন
# GitHub-এ গিয়ে "New Pull Request" করুন
```

### Commit Message Format

```
feat: নতুন feature যোগ করলে
fix: bug fix করলে
docs: documentation update
style: code formatting (logic change নেই)
refactor: code restructure (behavior change নেই)
test: test যোগ বা fix
chore: build, config update
```

### Contribution Ideas

- [ ] Nginx support
- [ ] PHP version selector per subdomain
- [ ] Automatic SSL (Let's Encrypt)
- [ ] Backup & restore functionality
- [ ] Two-factor authentication
- [ ] Site-level analytics
- [ ] Docker support
- [ ] Multi-admin user system
- [ ] Email notification system
- [ ] Subdomain traffic monitoring

### Code Guidelines

- PHP 8.0+ compatible syntax ব্যবহার করুন
- Security-sensitive functions-এ অবশ্যই input validation করুন
- নতুন feature-এর জন্য README update করুন
- Code-এ বাংলা/English দুটোই comment acceptable

---

## 🐛 Bug Report

কোনো bug বা সমস্যা পেলে **[GitHub Issues](https://github.com/websmartbd/devpack/issues)** এ report করুন।

### Bug Report করার আগে

1. Existing issues-এ search করুন (duplicate না হয়)
2. Latest version use করছেন কিনা check করুন
3. `config/config.php` settings ঠিক আছে কিনা verify করুন

### Bug Report-এ কী লিখবেন

```markdown
**Bug Description:**
[কী সমস্যা হচ্ছে তা স্পষ্টভাবে লিখুন]

**Steps to Reproduce:**
1. এই কাজটি করলাম...
2. তারপর এটা করলাম...
3. Error/সমস্যা দেখা গেল

**Expected Behavior:**
[কী হওয়া উচিত ছিল]

**Actual Behavior:**
[আসলে কী হচ্ছে]

**Environment:**
- OS: [e.g., Ubuntu 22.04]
- PHP: [e.g., 8.2]
- Apache: [e.g., 2.4.54]
- MySQL: [e.g., 8.0]
- SERVER_TYPE: [local/cpanel/vps]
- Browser: [e.g., Chrome 120]

**Error Log (if any):**
[data/.error_log এর content paste করুন]
```

**[🐛 Report a Bug](https://github.com/websmartbd/devpack/issues/new?labels=bug&template=bug_report.md)**
&nbsp;&nbsp;
**[💡 Request a Feature](https://github.com/websmartbd/devpack/issues/new?labels=enhancement&template=feature_request.md)**

---

## 📄 License

এই project [MIT License](LICENSE) এর অধীনে released।

```
MIT License — আপনি freely use, modify, এবং distribute করতে পারবেন।
Attribution দিলে ভালো হয় কিন্তু required নয়।
```

---

## 🙏 Acknowledgements

- [Tailwind CSS](https://tailwindcss.com) — UI styling
- [Remix Icon](https://remixicon.com) — Icons
- [JetBrains Mono](https://www.jetbrains.com/lp/mono/) — Monospace font
- [Inter](https://rsms.me/inter/) & [Plus Jakarta Sans](https://fonts.google.com/specimen/Plus+Jakarta+Sans) — Typography

---

<div align="center">

Made with ❤️ by [websmartbd](https://github.com/websmartbd)

⭐ **Star দিন যদি কাজে লেগে থাকে!** ⭐

</div>
