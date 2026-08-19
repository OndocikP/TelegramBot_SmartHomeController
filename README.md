# 🚪 Telegram Garage Controller

A simple and reliable **ESP32-based smart garage controller** that allows you to control your garage directly from **Telegram**.

The ESP32 connects to Wi-Fi and communicates with a Telegram bot. With a simple Telegram command, you can trigger the garage door remotely using a relay connected to the garage opener.

The project also includes user management, allowing you to control who has access to the garage.

---

## ✨ Features

* 📱 Control your garage directly from Telegram
* 🚪 Open or trigger the garage door with a simple command
* 🔐 User access control using Telegram `chat_id`
* 👤 Add and remove authorized users
* 📋 View the list of authorized users
* 💾 Store authorized users in ESP32 internal memory
* 📶 Automatic Wi-Fi connection
* 🔄 Automatic Telegram message processing
* ⚡ Fast relay activation
* 🖥️ Serial Monitor logging for easy monitoring
* 💡 Lightweight and easy to customize

---

## 🧰 Hardware

The project is designed around:

| Component          | Purpose               |
| ------------------ | --------------------- |
| ESP32              | Main controller       |
| Relay Module       | Garage opener control |
| Wi-Fi              | Internet connection   |
| Garage Door Opener | Garage door control   |

The relay is connected to **GPIO 4** by default.

```cpp
const int GARAGE_PIN = 4;
```

The relay is activated for **250 ms**, simulating a short button press on the garage opener.

---

## 🤖 Telegram Bot

The project uses a Telegram bot as the main user interface.

After creating your bot, simply add the Bot Token to the project:

```cpp
const char* botToken = "YOUR_BOT_TOKEN";
```

Once the ESP32 is connected to Wi-Fi, you can communicate with the garage directly through Telegram.

---

## 💬 Telegram Commands

### 🚪 `/garage`

Triggers the garage door.

```text
/garage
```

The ESP32 activates the relay for 250 ms and then sends a confirmation message back to Telegram.

---

### 🆔 `/chat`

Displays the current Telegram `chat_id`.

```text
/chat
```

This is useful when adding a new authorized user.

Example:

```text
Your chat ID: 123456789
```

---

### 🧪 `/test`

Tests communication between the Telegram bot and ESP32.

```text
/test
```

---

### 👥 `/list`

Displays all authorized users.

```text
/list
```

Example:

```text
📋 Authorized users:
- Admin : 123456789
- Peter : 987654321
```

---

### ➕ `/add`

Adds a new authorized user.

Format:

```text
/add Name chatId
```

Example:

```text
/add Peter 987654321
```

The user is added to the access list and stored in ESP32 memory.

---

### ➖ `/remove`

Removes an authorized user.

Format:

```text
/remove Name
```

Example:

```text
/remove Peter
```

---

## 🔐 User Management

The project includes a simple access-control system based on Telegram `chat_id`.

Before processing a command, the ESP32 checks whether the sender is an authorized user.

Authorized users are stored in a `std::map`:

```cpp
std::map<String, String> allowedChats;
```

Each user has a name and Telegram `chat_id`.

Example:

```text
Admin  → 123456789
Peter  → 987654321
```

This makes it easy to manage access directly from Telegram.

---

## 💾 Persistent Storage

Authorized users are stored using the ESP32 `Preferences` library.

This allows the project to keep the configured users in the ESP32's internal storage.

Users can be:

* ➕ Added
* ➖ Removed
* 📋 Listed
* 💾 Persistently stored

The user list is automatically loaded when the ESP32 starts.

---

## 📶 Wi-Fi

The ESP32 automatically connects to the configured Wi-Fi network.

Configuration:

```cpp
const char* ssid = "YOUR_WIFI_NAME";
const char* password = "YOUR_WIFI_PASSWORD";
```

The connection is also monitored during normal operation, allowing the ESP32 to reconnect when needed.

---

## 🔄 How It Works

```text
┌─────────────────┐
│     Telegram    │
│      User       │
└────────┬────────┘
         │
         │ /garage
         ▼
┌─────────────────┐
│  Telegram Bot   │
└────────┬────────┘
         │
         │ Internet
         ▼
┌─────────────────┐
│      ESP32      │
│                 │
│  User Check     │
│       ↓         │
│  GPIO Control   │
└────────┬────────┘
         │
         │ GPIO 4
         ▼
┌─────────────────┐
│      Relay      │
└────────┬────────┘
         │
         │ 250 ms pulse
         ▼
┌─────────────────┐
│  Garage Door 🚪 │
└─────────────────┘
```

---

## 🧩 Libraries

The project uses the following Arduino libraries:

```cpp
#include <WiFi.h>
#include <WiFiClientSecure.h>
#include <UniversalTelegramBot.h>
#include <Preferences.h>
#include <map>
```

### Main libraries

* **WiFi** — ESP32 Wi-Fi connectivity
* **WiFiClientSecure** — Secure network communication
* **UniversalTelegramBot** — Telegram Bot API communication
* **Preferences** — Persistent ESP32 storage
* **map** — User access management

---

## 🚀 Getting Started

### 1. Create a Telegram Bot

Create a Telegram bot using **BotFather** and get your Bot Token.

### 2. Configure Wi-Fi

Set your Wi-Fi credentials:

```cpp
const char* ssid = "YOUR_WIFI_NAME";
const char* password = "YOUR_WIFI_PASSWORD";
```

### 3. Configure the Telegram Bot

Add your Bot Token:

```cpp
const char* botToken = "YOUR_BOT_TOKEN";
```

### 4. Configure the Garage Relay

The default relay GPIO is:

```cpp
const int GARAGE_PIN = 4;
```

### 5. Upload to ESP32

Open the project in Arduino IDE, select your ESP32 board and upload the firmware.

### 6. Start Using Telegram

Open your Telegram bot and use:

```text
/garage
```

Your ESP32 will trigger the garage opener.

---

## 🏗️ Project Structure

```text
Telegram-Garage-Controller/
│
├── Telegram-Garage-Controller.ino
├── README.md
└── .gitignore
```

---

## 🌟 Why This Project?

The goal of this project is to create a **simple, practical and convenient smart garage controller** using hardware that is easy to obtain and software that is easy to understand.

Instead of creating a dedicated mobile application, Telegram provides a familiar interface that can be accessed from almost any device.

**ESP32 + Wi-Fi + Telegram + Relay = Smart Garage 🚪📱**

---

## 🔮 Future Ideas

The project can be extended with additional smart-home features such as:

* 📊 Garage door status
* 🔔 Garage notifications
* ⏱️ Automatic garage control
* 👥 Advanced user permissions
* 📝 Garage activity history
* 🌐 Web interface
* 🔘 Physical control button
* 🏠 Integration with other smart-home systems

---

## ❤️ Built With

**ESP32 · Arduino · Telegram Bot API · Wi-Fi · Relay**

A small IoT project that turns a regular garage into a **Telegram-controlled smart garage**. 🚪✨
