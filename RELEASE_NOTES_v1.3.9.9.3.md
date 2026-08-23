# AlertTicker Card — v1.3.9.9.3

## Bug fix — `{trigger_state}` / `{trigger_time}` empty in history, TTS, push ([#204](https://github.com/djdevil/AlertTicker-Card/issues/204))

Follow-up to v1.3.9.9.2.

### The bug

The trigger-state snapshot was captured **after** `_recordHistory()`, `_speakAlert()`, and `_pushNotifyAlert()` ran. So the very first message rendered by those consumers (the one that ends up in the History log, the TTS announcement, and the push notification body) saw an **empty** `_triggerStates` map and rendered:

- `{trigger_state}` → fallback to the current state (usually the same value, so it *looked* correct but was a coincidence)
- `{trigger_time}` → empty string
- `{trigger_attribute}` → empty string

### The fix

Snapshot capture is now performed **before** history/TTS/push are triggered. All three consumers now see the correct fire-time values on the first render.

### Timeline example after the fix

Alert config:
```yaml
- entity: light.studio
  operator: '!='
  state: 'ok'
  persistent: true
  message: '⚠️ Was {trigger_state} at {trigger_time} — currently {state}'
```

Sensor goes `ok` → `on` at 22:12 → alert fires → history log entry:
> ⚠️ Was on at 22:12 — currently on

Sensor returns to `off` → alert stays visible (persistent) → live message becomes:
> ⚠️ Was on at 22:12 — currently off

Previously the history entry was:
> ⚠️ Was on at  — currently on

Now the `at` timestamp is populated correctly.

---

## Upgrade

Replace `alert-ticker-card.js` and `alert-ticker-card-editor.js` with the v1.3.9.9.3 files and clear the browser cache.

[![Buy Me A Coffee](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/divil17f)
