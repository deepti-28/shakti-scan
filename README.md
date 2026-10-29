# ShaktiScan

**A women's safety and privacy app that helps detect hidden surveillance devices.**

ShaktiScan scans the Wi-Fi network you are connected to, identifies devices by vendor and open camera ports, scores each device by risk, and shows the result in simple heatmaps and alerts. It also includes an SOS feature for emergencies.

## Features

- **Wi-Fi / network analysis:** discovers devices on the connected network and shows IP, hostname, MAC address and vendor.
- **Surveillance device detection:** flags known camera vendors and suspicious camera ports (80, 554, 8000, 8080).
- **Risk scoring:** every device gets a risk level and a clear reason, so non-technical users can understand it quickly.
- **Real-time risk heatmap:** a visual view of risky and safe devices on the network.
- **IR lens scanning:** helps spot hidden camera lenses using the phone camera.
- **Offline scanning:** scanning features that keep working without an internet connection.
- **Automated alerts and SOS:** instant alerts for threats and a one-tap SOS for emergencies.

## Tech Stack

| Layer | Technology |
|---|---|
| Mobile app | Flutter, Dart, Kotlin |
| Backend API | Python, FastAPI, Uvicorn |
| Network scanning | Nmap (python-nmap), psutil |
| UI design | Figma, Stitch |

## Project Structure

```
shakti-scan/
├── backend/        # FastAPI backend (main.py)
├── lib/            # Flutter app source code
├── android/        # Android (Kotlin) platform code
├── pubspec.yaml    # Flutter dependencies
└── README.md
```

## Prerequisites

- [Flutter SDK](https://docs.flutter.dev/get-started/install) and Android Studio (with an emulator or a real Android phone)
- [Python 3.9+](https://www.python.org/downloads/)
- [Nmap](https://nmap.org/download.html) installed and added to PATH (on Windows, install it with Npcap)
- Git

## Run the Backend

Open a terminal (on Windows, **PowerShell as Administrator**, so MAC addresses and vendors can be read):

```powershell
cd backend
python -m venv venv
.\venv\Scripts\Activate.ps1
pip install fastapi "uvicorn[standard]" python-nmap psutil
python -m uvicorn main:app --reload
```

On macOS / Linux:

```bash
cd backend
python3 -m venv venv
source venv/bin/activate
pip install fastapi "uvicorn[standard]" python-nmap psutil
sudo python3 -m uvicorn main:app --reload
```

The server starts at `http://127.0.0.1:8000`.

- Interactive API docs: `http://127.0.0.1:8000/docs`
- Health check: `http://127.0.0.1:8000/health`

To let a real phone reach the backend, run it on all network interfaces:

```powershell
python -m uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

### API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET | `/` | Backend status |
| GET | `/health` | Health check |
| GET | `/scan` | Scans the connected Wi-Fi network and returns devices with risk scores |
| GET | `/heatmap` | Returns the scan result as heatmap data |
| GET | `/arp_scan/{network}` | ARP scan of a given network, e.g. `/arp_scan/192.168.1.0/24` |

## Run the Flutter App

From the project root:

```powershell
flutter pub get
flutter devices
flutter run -d <device-id>
```

For example: `flutter run -d emulator-5556`

### Connect the app to the backend

Set the backend base URL in the app's API configuration:

| Where the app runs | Base URL |
|---|---|
| Android emulator | `http://10.0.2.2:8000` |
| Real phone (same Wi-Fi as your PC) | `http://<your-pc-ip>:8000` (find it with `ipconfig`) |

When using a real phone, start the backend with `--host 0.0.0.0` and allow Python through Windows Firewall.

## Troubleshooting

- **`uvicorn` is not recognized:** run `python -m uvicorn main:app --reload` instead.
- **Nmap error or no devices found:** make sure Nmap is installed, on PATH, and the terminal is running as Administrator.
- **`Could not detect Wi-Fi network`:** connect the PC to Wi-Fi (Ethernet is not detected), and check the adapter name contains "Wi-Fi" or "WLAN".
- **Gradle cache or build errors:** run `flutter clean`, then `flutter pub get`, and try again.

## Screenshots


<img width="335" height="719" alt="image" src="https://github.com/user-attachments/assets/1d7075e6-7482-46b2-aba7-c0030547bf45" />
<img width="321" height="719" alt="image" src="https://github.com/user-attachments/assets/294636df-3cae-4ee1-a8bc-9a8dbdf2cb2b" />
<img width="332" height="714" alt="image" src="https://github.com/user-attachments/assets/49e7bf2f-c88a-47d9-8b5c-e1a942e11ec6" />



## Author

**Deepti Solanki**
GitHub: [deepti-28](https://github.com/deepti-28)
