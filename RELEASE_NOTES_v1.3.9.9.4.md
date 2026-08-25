# AlertTicker Card — v1.3.9.9.4

## 🎉 What's new

### 🔔 Push notifications, now with actions, custom sounds & critical alerts

Every alert can now send push notifications with **action buttons**, **custom sounds**, **critical alerts** (which bypass silent mode & Do Not Disturb), and much more.

**Real-world example:** you get a notification on your phone with two buttons — "Turn Off Light" and "Open Camera" — and you can act on it without even opening Home Assistant.

```yaml
push_notify: true
push_notify_service: mobile_app_iphone
push_notify_title: '💡 Studio'
push_notify_message: 'Light on since {trigger_time}'
push_notify_data:
  push:
    sound:
      name: Alarm.caf
      critical: 1
      volume: 1.0
    interruption-level: critical
  actions:
    - action: TURN_OFF_LIGHT
      title: 🔌 Turn Off
      destructive: true
    - action: URI
      title: 📸 View Camera
      uri: /lovelace/cameras
```

Everything is configurable from the **visual editor** too — a new YAML field appears inside each alert under the "Push notification" section.

Full README example includes a matching HA automation for handling the action button tap.

---

### ⚠️ New reminder: notifications need HA open in a browser

Added an amber notice in the editor (next to both the TTS and Push toggles) and in the README to make it clear that **TTS, push notifications, and sounds only fire while at least one browser tab has Home Assistant open** (desktop, wall tablet, or the HA Companion app in the foreground).

For 24/7 critical alerts (smoke, security, water leaks…) the right choice is still a **server-side HA automation**. The card's push/TTS is best used as a convenience layer on top.

Translated to all 12 supported languages.

---

### 🎨 New severity border control (thanks to [@sriramsv](https://github.com/sriramsv))

With `ha_theme: true`, each alert gets a coloured border based on its severity (red critical, orange warning, blue info, green ok). There's now a toggle to **disable it** while keeping the coloured badges and icons.

```yaml
severity_border: false
```

Great for users who want a flatter look without losing the colour coding.

---

## 📥 How to upgrade

- **Via HACS:** open HACS → Frontend → AlertTicker Card → Update
- **Manual:** replace `alert-ticker-card.js` and `alert-ticker-card-editor.js`

After updating, **clear your browser cache** (`Ctrl+F5`) so you see the new features right away.

---

## 🙏 Thanks

Special thanks to [@ShaneYu](https://github.com/ShaneYu) for suggesting the `push_notify_data` feature ([#207](https://github.com/djdevil/AlertTicker-Card/issues/207)) and to [@sriramsv](https://github.com/sriramsv) for the `severity_border` contribution ([#206](https://github.com/djdevil/AlertTicker-Card/pull/206)).

If this card is useful and saves you time, consider buying me a coffee — it's the best way to support continued development. ☕

[![Buy Me A Coffee](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/divil17f)
