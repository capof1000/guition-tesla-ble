# 🚗 Guition ESP32-S3 — Tesla BLE Gateway

> 🇫🇷 Français | [🇬🇧 English below](#-guition-esp32-s3--tesla-ble-gateway-1)

---

Interface tactile pour contrôler la recharge d'une Tesla via Bluetooth Low Energy, basée sur l'écran **Guition ESP32-S3 4848S040** et **ESPHome**.

---

## ✨ Fonctionnalités

- **Affichage de l'état de charge** — niveau de batterie en temps réel (arc + pourcentage)
- **Limite de recharge** — arc interactif ajustable directement sur l'écran
- **Contrôle de l'ampérage** — slider vertical + boutons +/- (mode manuel uniquement)
- **3 modes de charge** : Manuel / Solaire / Forcé
- **Image dynamique du véhicule** — 3 états : débranché / branché / en charge
- **Icônes WiFi et BLE dynamiques** — signal affiché par plage RSSI
- **Page paramètres** — luminosité, timeout, signal WiFi/BLE, uptime
- **Mise en veille automatique** — écran éteint après délai configurable
- **Restauration du mode de charge** après reboot

---

## 🖥️ Matériel requis

| Composant | Détail |
|-----------|--------|
| Écran | Guition ESP32-S3 4848S040 (4,8" tactile) |
| Connexion véhicule | Tesla (via BLE) |
| Intégration | Home Assistant + ESPHome |

---

## 🔗 Utilisation avec le Blueprint Tesla SmartCharge

Ce projet atteint son **plein potentiel** lorsqu'il est couplé au blueprint **Tesla SmartCharge** :

👉 **[capof1000/Tesla-SmartCharge](https://github.com/capof1000/Tesla-SmartCharge)**

[![Importer le blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://raw.githubusercontent.com/capof1000/Tesla-SmartCharge/refs/heads/main/Blueprint_TeslaSmartCharge.yaml)

### Ce que le blueprint apporte

Le blueprint pilote intelligemment la charge Tesla en fonction de :

- 🌞 La **production solaire** disponible
- 🏠 La **consommation du logement**
- 🔋 L'**état de charge (SOC)** du véhicule
- ⚡ Les **contraintes électriques** de l'installation (délestage automatique prioritaire)

### Modes disponibles

| Mode | Description |
|------|-------------|
| `manual` | Contrôle direct via l'écran (ampérage + start/stop) |
| `solar` | Piloté par le blueprint selon la production solaire |
| `forced` | Charge immédiate pilotée par le blueprint (avec sécurité délestage) |

### Lien avec le Guition

L'écran expose une entité `select` **Mode Charge Tesla** avec les valeurs `manual`, `solar`, `forced`, compatibles avec le blueprint v1.7. En mode `solar` ou `forced`, les boutons de contrôle manuel disparaissent de l'écran — c'est le blueprint qui prend la main.

---

## 📦 Dépendances

- **[esphome-tesla-ble (fork PedroKTFC)](https://github.com/PedroKTFC/esphome-tesla-ble/tree/repair)** — communication BLE Tesla
- **[guition-tesla-ble board](https://github.com/capof1000/guition-tesla-ble)** — configuration matérielle de l'écran

---

## ⚙️ Installation

### 1. Fichier `secrets.yaml`

```yaml
api_encryption_key: "VOTRE_CLE_API"
ble_mac_address: "XX:XX:XX:XX:XX:XX"
tesla_vin: "VOTRE_VIN"
```

### 2. Flash initial

Pour le premier flash, utilisez l'outil web ESPHome via USB :

👉 [web.esphome.io](https://web.esphome.io) — flashez le fichier `firmware.factory.bin`

### 3. Mises à jour suivantes

Les mises à jour s'effectuent en OTA via l'interface ESPHome.

---

## 🔧 Configuration

| Entité | Description | Défaut |
|--------|-------------|--------|
| `Screen GTW backlight` | Luminosité (55–100%) | 80% |
| `Screen GTW delay` | Timeout avant veille (15–3600s) | 60s |
| `Mode Charge Tesla` | Mode actif | manual |

---

## 📱 Interface

![Screen1](/images/screen1.png)

## 📝 Changelog

| Version | Changements |
|---------|-------------|
| b28 | Valeurs de mode en anglais pour compatibilité blueprint v1.7 |
| b27 | Boutons +/- et toggle visibles uniquement en mode manuel |
| b26 | Uniformisation du fond blanc |
| b25 | Suppression des bordures sur l'image centrale |
| b24 | Icône BLE : rafraîchissement par plage RSSI |
| b22 | Fix scroll barres supérieure/inférieure |
| b21 | Restauration du mode de charge après reboot |
| b20 | Ajout des modes manuel / solaire / forcé |
| b19 | Fix TPMS, migration vers fork repair |
| b18 | Slider ampérage vertical |
| b17 | Bouton start/stop superposé sur image centrale |
| b15 | Icône BLE dynamique |
| b14 | Icône WiFi dynamique |
| b13 | Fix sortie de veille écran |
| b11 | Anti-jitter sur l'arc de limite |
| b1  | Fix crash ESP + écran noir |

---

## 🐛 Problèmes connus

- En cas de crash ESP32, l'écran peut rester noir : débrancher/rebrancher l'alimentation.

---

## 🙏 Crédits

- **[PedroKTFC](https://github.com/PedroKTFC/esphome-tesla-ble)** — librairie esphome-tesla-ble
- **[ESPHome](https://esphome.io)** — framework
- **[Home Assistant](https://www.home-assistant.io)** — plateforme domotique

---
---

# 🚗 Guition ESP32-S3 — Tesla BLE Gateway

> [🇫🇷 Français ci-dessus](#-guition-esp32-s3--tesla-ble-gateway) | 🇬🇧 English

---

A touchscreen interface to control Tesla charging via Bluetooth Low Energy, built on the **Guition ESP32-S3 4848S040** display and **ESPHome**.

---

## ✨ Features

- **Live charge state display** — battery level in real time (arc + percentage)
- **Charge limit** — interactive adjustable arc directly on screen
- **Amperage control** — vertical slider + +/- buttons (manual mode only)
- **3 charge modes** : Manual / Solar / Forced
- **Dynamic vehicle image** — 3 states: unplugged / plugged / charging
- **Dynamic WiFi & BLE icons** — signal displayed by RSSI range
- **Settings page** — brightness, timeout, WiFi/BLE signal, uptime
- **Auto screen sleep** — screen turns off after configurable delay
- **Charge mode restored** after reboot

---

## 🖥️ Required Hardware

| Component | Details |
|-----------|---------|
| Display | Guition ESP32-S3 4848S040 (4.8" touchscreen) |
| Vehicle connection | Tesla (via BLE) |
| Integration | Home Assistant + ESPHome |

---

## 🔗 Use with the Tesla SmartCharge Blueprint

This project reaches its **full potential** when paired with the **Tesla SmartCharge** blueprint:

👉 **[capof1000/Tesla-SmartCharge](https://github.com/capof1000/Tesla-SmartCharge)**

[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://raw.githubusercontent.com/capof1000/Tesla-SmartCharge/refs/heads/main/Blueprint_TeslaSmartCharge.yaml)

### What the blueprint adds

The blueprint intelligently manages Tesla charging based on:

- 🌞 Available **solar production**
- 🏠 **Home energy consumption**
- 🔋 Vehicle **state of charge (SOC)**
- ⚡ **Electrical constraints** (automatic load shedding — always takes priority)

### Available modes

| Mode | Description |
|------|-------------|
| `manual` | Direct control from the screen (amperage + start/stop) |
| `solar` | Managed by the blueprint based on solar production |
| `forced` | Immediate charging managed by the blueprint (with load-shedding safety) |

### Integration with the Guition display

The screen exposes a `select` entity **Mode Charge Tesla** with values `manual`, `solar`, `forced`, compatible with blueprint v1.7. In `solar` or `forced` mode, the manual control buttons are hidden on screen — the blueprint takes over.

---

## 📦 Dependencies

- **[esphome-tesla-ble (PedroKTFC fork)](https://github.com/PedroKTFC/esphome-tesla-ble/tree/repair)** — Tesla BLE communication
- **[guition-tesla-ble board](https://github.com/capof1000/guition-tesla-ble)** — hardware board configuration

---

## ⚙️ Installation

### 1. `secrets.yaml` file

```yaml
api_encryption_key: "YOUR_API_KEY"
ble_mac_address: "XX:XX:XX:XX:XX:XX"
tesla_vin: "YOUR_VIN"
```

### 2. Initial flash

For the first flash, use the ESPHome web tool via USB:

👉 [web.esphome.io](https://web.esphome.io) — flash the `firmware.factory.bin` file

### 3. Subsequent updates

Updates are performed OTA via the ESPHome interface.

---

## 🔧 Configuration

| Entity | Description | Default |
|--------|-------------|---------|
| `Screen GTW backlight` | Brightness (55–100%) | 80% |
| `Screen GTW delay` | Sleep timeout (15–3600s) | 60s |
| `Mode Charge Tesla` | Active mode | manual |

---

## 📱 Interface

![Screen1](/images/screen1.png)

## 📝 Changelog

| Version | Changes |
|---------|---------|
| b28 | Mode values in English for blueprint v1.7 compatibility |
| b27 | +/- buttons and toggle hidden in non-manual modes |
| b26 | White background uniformization |
| b25 | Border removed from central image |
| b24 | BLE icon: refresh only on RSSI range change |
| b22 | Fix scroll on top/bottom bars |
| b21 | Charge mode restored after reboot |
| b20 | Added manual / solar / forced modes |
| b19 | Fix TPMS, migration to repair fork |
| b18 | Vertical amperage slider |
| b17 | Start/stop button overlaid on central image |
| b15 | Dynamic BLE icon |
| b14 | Dynamic WiFi icon |
| b13 | Fix screen wake from sleep |
| b11 | Anti-jitter on charge limit arc |
| b1  | Fix ESP crash + black screen |

---

## 🐛 Known Issues

- After an ESP32 crash, the screen may stay black: unplug and replug the power supply.

---

## 🙏 Credits

- **[PedroKTFC](https://github.com/PedroKTFC/esphome-tesla-ble)** — esphome-tesla-ble library
- **[ESPHome](https://esphome.io)** — framework
- **[Home Assistant](https://www.home-assistant.io)** — home automation platform


