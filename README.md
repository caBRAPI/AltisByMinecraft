<div align="center">

# Altis

<img src="https://www.cabrapi.com.br/images/banner/banner-icon-name-dark.webp" alt="caBRAPI" width="320"/>

**Official caBRAPI plugin for Spigot/Paper servers.**

Automatically integrates purchases made on the **caBRAPI** platform into your Minecraft server.

<br>

<a href="https://github.com/caBRAPI/cabrapi-minecraft/releases">
    <img alt="Version" src="https://img.shields.io/badge/Version-1.0.0-white"/>
</a>

<a href="https://opensource.org/licenses/Apache-2.0">
    <img alt="License" src="https://img.shields.io/badge/License-Apache%202.0-white.svg"/>
</a>

<img alt="Platform" src="https://img.shields.io/badge/Platform-Spigot%20%7C%20Paper-white"/>

</div>

## ✨ Features

- Automatic synchronization of caBRAPI purchases.
- Automatic product delivery.
- Execution of custom commands.
- Compatible with **Spigot** and **Paper**.
- Compatible with **nLogin**.
- Full inventory check.
- Webhook (Discord) notifications.
- Compatible with versions: `1.16.x`, `1.17.x`, `1.18.x`, `1.19.x`, `1.20.x`, `1.21.x`, `26.x`


## 📦 Installation

1. Download the latest version from **Releases**.
2. Place the `.jar` file in the `plugins/` folder.
3. Start or restart the server.
4. Configure the file: `plugins/altis/config.yml`

## ⚙️ Configuration

```yaml
# ========================================
# Altis - Configuration
# ========================================

# Check for available plugin updates.
check-update: true

# Configuration version (do not change).
version: 1

# Interval in minutes to check pending payments (console mode).
check-interval: 5

# Your store API key.
# You can get it in the caBRAPI panel.
api-key: ""

# Your store ID.
# Available in the caBRAPI admin panel.
store-id: ""

# ========================================
# Discord Webhook
# ========================================
# Available variables in "message":
#   {player}   -> Player name
#   {products} -> Product name(s) (e.g. "10x DEMONSTRATION")
webhook:
  enable: false
  url: ""
  message: "{player} bought {products} in the store!"

# ========================================
# In-Game Messages
# ========================================
# Available variables in all messages:
#   {player}   -> Player name
#   {product}  -> Product name
#   {quantity} -> Amount purchased
#   {count}    -> Payments activated
#   {total}    -> Total payments found
#   {status}   -> HTTP status code
#   {error}    -> Error message
#   {current}  -> Current plugin version
#   {latest}   -> Latest available version
#   {paymentId} -> Payment ID
# Available colors:
#   &0 Black    &1 Dark Blue  &2 Dark Green &3 Dark Cyan
#   &4 Red &5 Purple         &6 Gold      &7 Light Gray
#   &8 Gray    &9 Blue         &a Green        &b Cyan
#   &c Red &d Magenta     &e Yellow      &f White
message:
  # ========================================
  # Messages for the Player
  # ========================================
  permission: "&c&l[ALTIS] &cYou do not have permission."
  inventory: "&e&l[ALTIS] &eYour inventory is full! You need at least &f{slots} &eempty slot(s) to receive your items."
  reload: "&a&l[ALTIS] &aConfiguration reloaded successfully!"
  activation-success: "&a&l[ALTIS] &a{count} payment(s) activated successfully!"

  # ========================================
  # Startup Status (Console)
  # ========================================
  api-key-configured: "&aConfigured"
  api-key-not-configured: "&cNot configured"
  store-id-configured: "&aConfigured"
  store-id-not-configured: "&cNot configured"
  configure-credentials: "&cNote: &fConfigure &capi-key &fand &cstore-id &fin the &bconfig.yml&f file."
  nlogin-detected: "&fnLogin: &aDetected"
  nlogin-not-found: "&fnLogin: &eNot found &8- &7using PlayerJoinEvent."

  # ========================================
  # Console - Activation
  # ========================================
  activation-log: "&aActivated &f{count}/{total} &apayment(s) for &f{player}"
  reload-by: "&aConfiguration reloaded by &f{player}"

  # ========================================
  # Console - Services
  # ========================================
  nlogin-event-received: "&anLogin event received for &f{player}"
  no-pending-payments: "&eNo pending payments for &f{player}"
  api-request-error: "&cNote: &fAPI returned &e{status} &ffor &b{player}"
  payment-update-failed: "&cNote: &fFailed to update payment &e{paymentId}&f: HTTP &e{status}"
  payment-update-error: "&cNote: &fError updating payment &e{paymentId}&f: &7{error}"
  metadata-fetch-error: "&cNote: &fError fetching payment metadata &e{paymentId}&f: &7{error}"
  product-fetch-error: "&cNote: &fError fetching product: &7{error}"
  command-executed: "&aExecuting: &f{command} &7(x{quantity}) &afor &f{player} &7via &f{executor}"
  webhook-sent: "&aWebhook notification sent to Discord: &f{player}"
  webhook-failed: "&cNote: &fFailed to send webhook: &7{error}"

  # ========================================
  # Console - Version Checker
  # ========================================
  update-check-failed: "&cNote: &fCould not check for updates (HTTP &e{status}&f)."
  update-check-invalid: "&cNote: &fCould not check for updates. Invalid response."
  update-available: "&eNote: &fA new version is available! &a(v{current} → v{latest})"
  update-current: "&aYou are using the latest version. &f(v{version})"
  update-download: "&fDownload: &bhttps://github.com/caBRAPI/cabrapi-minecraft/releases"
  update-check-error: "&cNote: &fCould not check for updates. &7{error}"

  # ========================================
  # Console - Config Version
  # ========================================
  config-outdated: "&eNote: &fYour config.yml is outdated (v{current}). It is recommended to update it to version v{latest}."
  config-newer: "&eNote: &fYour config.yml seems to be from a newer version (v{current}). If there are issues, check the configurations."

```

## 📜 Commands

|    Permission     |      Command      |            Description                |
|------------------|-------------------|-------------------------------------|
| `cabrapi.admin`  | `/cabrapi reload` | Reloads the plugin configuration. | 
```