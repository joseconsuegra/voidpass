# VoidPass 🚀 

**VoidPass** is a lightweight, 100% serverless, peer-to-peer (P2P) file transfer web application. It allows you to securely send files of any size directly from one browser to another using WebRTC, without ever uploading your data to an intermediate cloud server.

## ✨ Features

* **Serverless Privacy:** Files travel directly between the sender and receiver via WebRTC Data Channels. No files are ever stored on or routed through a central server.
* **No File Size Limits (GB+ Support):** Instead of loading the entire file into RAM, VoidPass reads and sends the file in manageable 1MB chunks (Ping-Pong flow).
* **Direct-to-Disk Streaming:** For supported browsers (Chrome, Edge, Opera), it uses the modern **File System Access API** to write chunks directly to the hard drive as they arrive, meaning you can receive 50GB+ files using almost zero RAM. (Includes a RAM fallback for Firefox/Safari).
* **Rich Clipboard Sharing:** Copies both the shareable URL and the generated QR Code image simultaneously. You can paste them directly into WhatsApp, Slack, Telegram, or Teams in a single click.
* **Zero Dependencies / Single File:** The entire application is contained within a single `index.html` file. 

## 🛠️ How It Works

1. **Signaling:** The app uses [PeerJS](https://peerjs.com/) to connect to a free public signaling server. This server is *only* used for the initial "handshake" (exchanging IPs/Ports) between the two browsers.
2. **P2P Connection:** Once the handshake is complete, a direct WebRTC connection is established.
3. **Transfer:** The sender chunks the file and sends it directly to the receiver. The receiver acknowledges each chunk before the next one is sent.

## 🚀 How to Run Locally

Due to browser security policies regarding WebRTC and the Clipboard/File System APIs, **you cannot run this app by simply double-clicking the HTML file** (using the `file:///` protocol). It must be served over HTTP/HTTPS.

### Option A: VS Code (Recommended)
1. Install the [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) extension.
2. Open `index.html` in VS Code.
3. Right-click anywhere in the code and select **"Open with Live Server"**.

### Option B: Python
If you have Python installed, open your terminal/command prompt in the project folder and run:
```bash
# Python 3
python -m http.server 8000
```
Then, open your browser and navigate to http://localhost:8000.

### Option C: Host it for free

Since it's a static site, you can instantly deploy it for free on platforms like:
* GitHub Pages
* Vercel
* Netlify

## 🌐 Browser Compatibility

| Feature | Chrome / Edge / Opera | Firefox | Safari |
| :--- | :---: | :---: | :---: |
| **WebRTC P2P Transfer** | ✅ Supported | ✅ Supported | ✅ Supported |
| **Direct-to-Disk Streaming** | ✅ Supported | ⚠️ Fallback to RAM | ⚠️ Fallback to RAM |
| **Rich Clipboard (Text + Image)**| ✅ Supported | ⚠️ Text Only | ✅ Supported |

*Note: On browsers that do not support the File System Access API (like Firefox), large files are held in RAM until the transfer completes. Receiving extremely large files (several GBs) on these browsers may cause the tab to crash.*

## 💻 Built With

* **HTML5, CSS3, Vanilla JavaScript**
* [**PeerJS**](https://peerjs.com/) - WebRTC wrapper and free signaling server.
* [**QRCode.js**](https://davidshimjs.github.io/qrcodejs/) - Cross-browser QR code generation.

## 📄 License

This project is open-source and available under the [MIT License](LICENSE).

