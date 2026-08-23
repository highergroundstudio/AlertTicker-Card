# AlertTicker Card — v1.3.9.9.2

## What's new

### 🎯 New message placeholders — remember what triggered the alert ([#204](https://github.com/djdevil/AlertTicker-Card/issues/204))

Three new placeholders capture the entity state **at the moment the alert first fires** and keep it available for the entire life of the alert:

| Placeholder | Value |
|-------------|-------|
| `{trigger_state}` | The state the entity had when the alert became active |
| `{trigger_attribute}` | Attribute value at fire time (when `attribute:` is set) |
| `{trigger_time}` | Local time string of when the alert first fired |

### Why this matters

For **persistent alerts** (`persistent: true`), the underlying sensor can return to normal but the alert stays visible until the user dismisses it. Previously the `{state}` placeholder would show the *current* state (e.g. `"ok"`), losing the information about what actually triggered the alert (`"critical"`).

Now you can build messages like:

```yaml
- entity: sensor.system_status
  operator: '!='
  state: 'ok'
  persistent: true
  message: '⚠️ Was {trigger_state} at {trigger_time} — currently {state}'
```

**Timeline example:**
1. Sensor goes from `ok` → `critical` → alert fires with message *"⚠️ Was critical at 14:32 — currently critical"*
2. Sensor recovers to `ok` → alert stays visible (persistent), message becomes *"⚠️ Was critical at 14:32 — currently ok"*
3. User dismisses the persistent alert → snapshot is cleared

### Persistence

Trigger snapshots are stored in `localStorage` (key `atc-trigger-states`), so they survive page reloads. When an alert clears (state condition no longer matches, or dismissal), the snapshot is automatically deleted.

---

### Also available — already supported before this release

For alerts with **multiple matching states** (e.g. `operator: '!='` matching `warning`, `critical`, `unknown`), you can already use the existing `{state}` placeholder or full Jinja2 templates to render different messages per state:

```yaml
- entity: sensor.system_status
  operator: '!='
  state: 'ok'
  message: >
    {% if is_state(entity, 'critical') %}
      🚨 CRITICAL on {{ area_name(entity) }}
    {% elif is_state(entity, 'warning') %}
      ⚠️ Warning: {{ states(entity) }}
    {% else %}
      ℹ️ Status: {state}
    {% endif %}
```

One alert, many messages. No duplication needed.

---

## Upgrade

Replace `alert-ticker-card.js` and `alert-ticker-card-editor.js` with the v1.3.9.9.2 files and clear the browser cache.

[![Buy Me A Coffee](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/divil17f)
