# IoT Door Camera with ESP32-CAM

A smart door camera system built with ESP32-CAM and ESPHome, providing real-time video streaming and snapshot capabilities with Home Assistant integration.

## 🚀 Features

- **Live Video Streaming**: Real-time camera feed on port 81
- **Snapshot Mode**: Capture still images on port 82
- **Home Assistant Integration**: Seamless API integration with encrypted communication
- **WiFi Connectivity**: Automatic connection with fallback hotspot
- **Remote Management**: OTA (Over-The-Air) updates and remote restart
- **LED Flash Control**: Built-in flash/illumination control
- **System Monitoring**: WiFi signal strength and uptime tracking

## 📋 Prerequisites

- Python 3.10 or higher
- ESP32-CAM module
- Home Assistant (optional, for full integration)
- WiFi network credentials

## 🛠️ Hardware Setup

### ESP32-CAM Pin Configuration

- **Camera Pins**: GPIO5, GPIO18, GPIO19, GPIO21, GPIO36, GPIO39, GPIO34, GPIO35
- **I2C Pins**: SDA (GPIO26), SCL (GPIO27)
- **External Clock**: GPIO0 (20MHz)
- **VSYNC**: GPIO25
- **HREF**: GPIO23
- **Pixel Clock**: GPIO22
- **Power Down**: GPIO32
- **LED Flash**: GPIO4

## 📦 Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd iot-doorcam
   ```

2. **Create a virtual environment (recommended)**
   ```bash
   python3.10 -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Configure secrets**
   
   Create a `secrets.yaml` file in the project root with the following structure:
   ```yaml
   wifi_ssid: "your_wifi_ssid"
   wifi_password: "your_wifi_password"
   api_eencryption: "your_api_encryption_key"
   ota_password: "your_ota_password"
   ap_password: "your_fallback_ap_password"
   ```

## 🔧 Configuration

The main configuration is in `esp32-cam.yaml`. Key settings include:

- **Resolution**: 640x480 (configurable)
- **Max Framerate**: 10 fps
- **Idle Framerate**: 0.1 fps
- **Web Server Ports**:
  - Port 81: Streaming mode
  - Port 82: Snapshot mode

## 🚀 Deployment

1. **Validate the configuration**
   ```bash
   esphome config esp32-cam.yaml
   ```

2. **First-time flash (via USB)**
   ```bash
   esphome run esp32-cam.yaml
   ```

3. **Over-The-Air updates (after initial flash)**
   ```bash
   esphome run esp32-cam.yaml --device <esp32-cam-ip-address>
   ```

## 📡 Usage

After successful deployment:

1. **Access Live Stream**: `http://<esp32-cam-ip>:81`
2. **Access Snapshots**: `http://<esp32-cam-ip>:82`
3. **Monitor in Home Assistant**: The device will automatically appear in your Home Assistant instance

### Available Entities in Home Assistant

- **Camera**: ESP32 CAM (main camera feed)
- **Light**: Camera Flash (LED control)
- **Sensor**: WiFi Signal Strength
- **Sensor**: Uptime
- **Switch**: Restart

## 🔒 Security Features

- API encryption for Home Assistant communication
- OTA password protection
- Fallback AP with password protection
- Secrets stored separately from main configuration

## 📚 Technical Specifications

- **Framework**: ESP-IDF
- **Board**: ESP32-DEV
- **ESPHome Version**: 2025.7.5
- **Python Version**: 3.10+
- **Camera Resolution**: 640x480 (QVGA)
- **Clock Frequency**: 20MHz

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

## 🔗 Resources

- [ESPHome Documentation](https://esphome.io/)
- [ESP32-CAM Guide](https://esphome.io/components/esp32_camera.html)
- [Home Assistant](https://www.home-assistant.io/)

## ⚠️ Notes

- Ensure adequate power supply for ESP32-CAM (minimum 5V 2A recommended)
- The web server component is currently commented out in favor of the camera-specific web server
- Keep your `secrets.yaml` file secure and never commit it to version control
