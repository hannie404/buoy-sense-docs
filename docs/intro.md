---
sidebar_position: 1
---

# Welcome to BuoySense Documentation

![BuoySense](https://github.com/user-attachments/assets/033d04e6-19b5-4a32-be69-ef9e7eeeca58)

Welcome to the **BuoySense** documentation! This comprehensive guide will help you understand, integrate, and extend our IoT flood monitoring system.

## What is BuoySense?

BuoySense is a real-time IoT flood monitoring system that provides:

- 🌊 **Real-time Water Level Monitoring** across multiple rivers and waterways
- 📡 **LoRa-based Communication** for reliable long-range data transmission
- 🗺️ **Interactive Mapping** with live weather overlays
- 📊 **Advanced Analytics** with predictive flood risk assessment
- 🔔 **Smart Alerts** for critical water level changes
- 📱 **Responsive Dashboard** for desktop and mobile devices

## Key Features

### For Users
- Real-time dashboard with live sensor data
- Interactive 3D buoy visualization
- Comprehensive analytics and reporting
- Customizable alerts and notifications
- Multi-format data export (CSV, JSON, PDF)

### For Developers
- RESTful API for buoy data access
- WebSocket support for real-time updates
- LoRa gateway integration
- Extensible architecture
- Well-documented endpoints

## Quick Start

Choose your path:

- 👤 **End Users**: Start with the [Installation Guide](./installation)
- 💻 **Developers**: Jump to the [API Reference](./api-reference/)
- 🔧 **System Administrators**: Check the [Installation Guide](./installation)
- 🤝 **Contributors**: Read the documentation and submit PRs on GitHub

## System Architecture

```
┌─────────────────┐
│   IoT Buoys     │ (LoRa Sensors)
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  LoRa Gateway   │ (Data Collection)
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│   API Server    │ (Data Processing)
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│   Dashboard     │ (Web Interface)
└─────────────────┘
```

## Technology Stack

- **Frontend**: Next.js 16, TypeScript, Tailwind CSS
- **3D Graphics**: Three.js, React Three Fiber
- **Maps**: Mapbox GL, OpenWeather API
- **Charts**: Recharts
- **IoT**: LoRa 915MHz, HC-SR04, MPU-6050
- **Database**: PostgreSQL (recommended)
- **Deployment**: Vercel, Docker

## Need Help?

- 📖 Browse the documentation sections
- 💬 Join our community discussions
- 🐛 Report issues on [GitHub](https://github.com/hannie404/buoy-dashboard)
- 📧 Contact: support@buoysense.com

## License

BuoySense is open source and available under the MIT License.

---

**Ready to get started? Continue to the next section!** →
