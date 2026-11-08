# CHANGELOG

All significant changes to this project will be documented in this file.

## [1.1.0] - 2026-07-14
### Added
- **Dual product execution system**: `run` field in product metadata (`"console"` or `"player"`)
  - `console` (default): Commands executed by the console, no inventory check
  - `player`: Commands executed by the player, with inventory check when enabled
- **Periodic console payment check**: Async task runs every `check-interval` minutes (default 5) processing pending payments for console mode products
- **Persisted processed payments**: `data/processed.yml` file records all processed purchases with complete details
- **Complete Javadocs**: Java documentation added to all project files (7 classes)
- **Configurable inventory slot**: `inventory.slot` field defines the minimum empty slots required
  - Values below 1 are adjusted to 1 (minimum)
  - Values above 36 are adjusted to 36 (player inventory maximum)
- **Detailed command logging**: Each executed command is logged with name, quantity and executor
- **Decimal support in check-interval**: Accepts `0.5` (30 seconds), `0.25` (15 seconds), etc.

### Changed
- **100% messages configuration**: All plugin messages are configurable via `config.yml` (25+ keys)
- **Logger without forced colors**: Removed `&e`, `&c`, `&f` codes from Logger; colors come exclusively from config.yml
- **Conditional LoginListener**: Listener registered only when nLogin is NOT present (previously always registered)
- **VersionChecker updated**: Constructor now receives `ActivatorPlugin` to access configuration
- **Webhook message clarified**: Message "Webhook notification sent to Discord: {player}" (about the player, not to them)
- **Inventory check on main thread**: Inventory check runs via `callSyncMethod` for safe inventory access
- **Race condition fixed**: `CountDownLatch` ensures products are dispatched before marking API as delivered
- **Products first, API after**: Product dispatch happens before API update (avoids loss in case of crash)
- **Duplicate payment prevented**: ID saved to file even if API update fails (avoids double delivery)

### Fixed
- **Thread safety**: `ConcurrentHashMap.newKeySet()` for `processedPayments` (previously a common HashSet)
- **Fallback nickname for console**: `filterPendingPayments(null)` now accepts null to fetch all pending
- **Product without run mode**: Default `getProductRunMode()` returns `"console"` when metadata does not define `run`

### Removed
- **Emojis from messages**: Removed ✔ and ✘ from all messages
- **Redundant fields in Logger**: Removed unused fields and methods

### Config
```yaml
# New keys added to config.yml
check-interval: 5  # Interval in minutes for periodic check
```

### Product Metadata
```json
{
  "minecraft": {
    "run": "console",       // "console" (default) or "player"
    "commands": ["give {player} diamond 1"],
    "message": "&aYou received a diamond!",
    "inventory": {
      "enable": false,      // Only works when run = "player"
      "slot": 4             // Minimum empty slots (1-36, default 1)
    }
  }
}
```

### Processed Payments Record (data/processed.yml)
```yaml
payments:
  "payment-abc123":
    player: "Steve"
    uuid: "player-uuid"     # Empty for console mode
    api-updated: true
    timestamp: "14/07/2026 15:30:00"
    products:
      - "1x VIP"
      - "2x Surprise Box"
  "payment-def456":
    player: "Alex"
    uuid: ""                     # Empty (processed by console)
    api-updated: true
    timestamp: "14/07/2026 15:35:00"
    products:
      - "1x Coins"
```
