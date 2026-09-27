# WiFi File Transfer — Windows 📡

Transfer files between your PC, phone, and other devices on the same WiFi network.  
No cables, no cloud, no accounts — just a URL.

## 🚀 Quick Start

### Prerequisites

1. **Install Python 3.8+** from [python.org/downloads](https://www.python.org/downloads/)  
   ⚠️ **Important:** Check ✅ **"Add Python to PATH"** during installation

### Run

**Option A — Double-click** `server.bat`

**Option B — Command Prompt:**
```cmd
git clone https://github.com/TJeyesh/wifi-transfer-windows.git
cd wifi-transfer-windows
server.bat start
```

That's it! The script will:
1. Create a virtual environment (if needed)
2. Install dependencies automatically
3. Start the server
4. Print the URL to open on other devices

### Transfer Files

1. Open the **Network URL** on any device connected to the same WiFi
2. Upload files via drag & drop, or use the **⚡ Fast Upload** for large files
3. Download files from the file list

## ✨ Features

- **📱 Cross-device** — Share files between your phone and PC
- **⚡ Fast Upload** — Direct HTTP upload endpoint bypasses Streamlit for maximum speed
- **📷 QR Code** — Scan to open on your phone instantly
- **🔒 Local only** — Files never leave your network
- **🎨 Beautiful UI** — Modern dark theme with glassmorphism

## 📋 Commands

```cmd
server.bat start       REM Start the server
server.bat stop        REM Stop the server
server.bat restart     REM Restart the server
server.bat status      REM Check if the server is running
server.bat install     REM Install/update dependencies
server.bat             REM Interactive menu (or double-click)
```

## 🏗️ Architecture

| Component | Port | Purpose |
|-----------|------|---------|
| Streamlit App | 8501 | Main UI — file list, QR codes, upload |
| File Server | 8502 | Direct HTTP downloads + Fast Upload |

### Fast Upload (Port 8502)

For large files, the **Fast Upload** page at `http://<your-ip>:8502/upload` bypasses Streamlit entirely:
- Raw HTTP POST — no multipart encoding overhead
- Streams directly to disk in 256 KB chunks
- Multi-threaded — parallel uploads/downloads
- Real-time speed indicator and progress bars

## 📁 Project Structure

```
wifi-transfer-windows/
├── app.py                # Main Streamlit application
├── server.bat            # Windows launcher (double-click to run)
├── requirements.txt      # Python dependencies
├── .streamlit/
│   └── config.toml       # Streamlit configuration
└── static/               # Uploaded files stored here (git-ignored)
```

## ⚙️ Requirements

- **Python 3.8+** — [Download](https://www.python.org/downloads/) (check "Add to PATH")
- Both devices must be on the **same WiFi network**

### Troubleshooting

- **"python is not recognized"** → Re-install Python with "Add to PATH" checked
- **Windows Firewall prompt** → Click **Allow access** so other devices can connect
- **Port already in use** → Run `netstat -ano | findstr :8501` and kill the process
- **Antivirus blocking** → Add the project folder to your antivirus exceptions

## 📄 License

MIT
