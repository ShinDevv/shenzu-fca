# SHENZU-FCA
---

## 🚀 Getting Started

To use this library, you need an `appstate.json` containing your Facebook session cookies.

### 1. Basic Setup
```javascript
const { login } = require("./module/index");
const fs = require("fs");

const credentials = { appState: JSON.parse(fs.readFileSync("appstate.json", "utf8")) };

login(credentials, {}, (err, api) => {
    if (err) return console.error(err);
    
    // Your bot logic here
});
```

---

## 💬 Messaging API

### `api.sendMessage(msg, threadID, callback, messageID)`
Sends a message to a specific thread.

```javascript
api.sendMessage("Hello from SHENZU-FCA!", event.threadID);

// With reply
api.sendMessage("This is a reply", event.threadID, event.messageID);

// With attachments
api.sendMessage({
    body: "Check this out!",
    attachment: fs.createReadStream("./image.jpg")
}, event.threadID);
```

### `api.sendMessageMqtt(msg, threadID, messageID)`
A faster way to send messages using the MQTT protocol.

```javascript
api.sendMessageMqtt("Fast message via MQTT", event.threadID);
```

### `api.setMessageReaction(reaction, messageID)`
React to a message (e.g., ❤️, 👍, 😆).

```javascript
api.setMessageReaction("❤️", event.messageID);
```

---

## 🔔 Real-time Events

### `api.listenMqtt(callback)`
Listens for real-time events like messages, reactions, and typing indicators.

```javascript
api.listenMqtt((err, event) => {
    if (err) return console.error(err);
    
    if (event.type === "message") {
        console.log(`Message from ${event.senderID}: ${event.body}`);
    }
});
```

---

## 🛠️ Other Functionalities

- **`api.getUserInfo(userID, callback)`**: Get detailed information about a user.
- **`api.getThreadInfo(threadID, callback)`**: Get information about a group or private chat.
- **`api.sendTypingIndicator(threadID, callback)`**: Show the "typing..." status.
- **`api.unsendMessage(messageID)`**: Remove a message sent by the bot.

## 🚀 Deployment via GitHub Actions

This repository is configured to automatically publish to NPM whenever you push to the `main` branch.

### **Setup Instructions:**
1.  **Get an NPM Token:** Go to [npmjs.com](https://www.npmjs.com/), navigate to **Access Tokens**, and create a new **Automation** token.
2.  **Add to GitHub Secrets:** 
    *   In your GitHub repository, go to **Settings** > **Secrets and variables** > **Actions**.
    *   Create a new repository secret named `NPM_TOKEN` and paste your token there.
3.  **Push to Main:** Once you push your code to the `main` branch, GitHub Actions will handle the publication automatically.


This library is a modified version of **ws3-fca**.

**Original Owners & Developers:**
- **Kenneth Aceberos** (@NethWs3Dev) - Main Developer
- **Exocore Community** - Foundational Architecture

**Modified by:**
- **SHENZU**

---

## 📊 License
Licensed under the **MIT License**.
