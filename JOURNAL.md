# Build Journal — WiFi Scanner (ESP32)

## Day 1 — Getting Started

Started the project by setting up the ESP32 with VS Code and Arduino CLI on my Mac. 
Wrote the base sketch using `WiFi.h` to scan for nearby networks and print them 
to the Serial Monitor — SSID, RSSI (signal strength), and encryption type for 
each network found.

**Goal:** Have the ESP32 continuously scan and list all WiFi networks in range.

## Uploading Issues

Hit an upload error right away:
Turned out the Serial Monitor was still open in another tab, which locked the 
port so `arduino-cli upload` couldn't access it. Closed the monitor, reconnected 
the USB cable, and the upload went through fine.

**Lesson learned:** Always close the Serial Monitor before uploading — the port 
can only be used by one process at a time.

## Getting the Scan Working

Once uploaded, the scan loop worked as expected:
- `WiFi.scanNetworks()` returns the number of networks found
- Looped through each network printing SSID, RSSI, and whether it's open or 
  encrypted (`WIFI_AUTH_OPEN` check)
- Added a short delay between scans so the serial output doesn't spam too fast

## Testing

Ran the scanner near my house and confirmed it picks up:
- My home network
- Neighboring networks
- Open/guest networks

Signal strength readings matched what I'd expect — closer networks showed 
stronger (less negative) RSSI values, e.g. -45 dBm vs -78 dBm for farther ones.

## What's Next / Possible Improvements
- Add an OLED or LCD display instead of relying on Serial Monitor
- Sort networks by signal strength before printing
- Add a button to trigger scans on demand instead of looping automatically
- Explore averaging RSSI over multiple scans for more stable readings

## Final Result
A working ESP32 WiFi scanner that continuously detects and lists nearby 
networks with signal strength and security info, viewable through the 
Serial Monitor.
