# AlertTicker Card — v1.3.9.9.4

## 🎉 What's new

### 🔔 Notifiche push potenziate — azioni, suoni personalizzati, allarmi critici

Ora ogni alert può inviare notifiche push con **pulsanti di azione**, **suoni personalizzati**, **allarmi critici** (che bypassano la modalità silenziosa e Non Disturbare) e molto altro.

**Esempio pratico:** ricevi una notifica sul telefono con due pulsanti — "Spegni Luce" e "Apri Camera" — e puoi agire senza aprire Home Assistant.

```yaml
push_notify: true
push_notify_service: mobile_app_iphone
push_notify_title: '💡 Studio'
push_notify_message: 'Luce accesa da {trigger_time}'
push_notify_data:
  push:
    sound:
      name: Alarm.caf
      critical: 1
      volume: 1.0
    interruption-level: critical
  actions:
    - action: TURN_OFF_LIGHT
      title: 🔌 Spegni
      destructive: true
    - action: URI
      title: 📸 Vedi Camera
      uri: /lovelace/cameras
```

Tutto è configurabile anche dall'editor visuale — c'è un nuovo campo YAML dentro ogni alert nella sezione "Notifica Push".

---

### ⚠️ Nuovo avviso: le notifiche funzionano solo con Home Assistant aperto

Aggiunto un promemoria arancione nell'editor (accanto ai toggle TTS e Push) e nel README per chiarire che **TTS, notifiche push e sound funzionano solo mentre almeno una scheda del browser ha Home Assistant aperto** (desktop, tablet fisso, o app Companion in primo piano).

Per allarmi critici 24/7 (fumo, sicurezza, allagamenti) la scelta giusta resta sempre creare un'**automazione HA lato server**.

Tradotto in tutte e 12 le lingue supportate.

---

### 🎨 Nuovo controllo bordo severità (grazie a [@sriramsv](https://github.com/sriramsv))

Con `ha_theme: true` ogni alert riceve un bordo colorato in base alla severità (rosso critical, arancione warning, blu info, verde ok). Ora c'è un toggle per **disattivarlo** mantenendo colorati badge e icone.

```yaml
severity_border: false
```

Utile per chi vuole un look più "flat" senza perdere il codice colore.

---

## 📥 Come aggiornare

- **Via HACS:** apri HACS → Frontend → AlertTicker Card → Aggiorna
- **Manuale:** sostituisci i file `alert-ticker-card.js` e `alert-ticker-card-editor.js`

Dopo l'aggiornamento, **svuota la cache del browser** (`Ctrl+F5`) per vedere subito le novità.

---

## 🙏 Grazie

Un grazie speciale a [@ShaneYu](https://github.com/ShaneYu) per aver proposto la feature `push_notify_data` ([#207](https://github.com/djdevil/AlertTicker-Card/issues/207)) e a [@sriramsv](https://github.com/sriramsv) per il contributo su `severity_border` ([#206](https://github.com/djdevil/AlertTicker-Card/pull/206)).

Se questa card ti è utile e ti fa risparmiare tempo, considera di offrirmi un caffè — è il modo migliore per sostenere lo sviluppo continuo. ☕

[![Buy Me A Coffee](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/divil17f)
