# Installation Guide

This guide will help you set up BuoySense on your local machine or server.

## Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js** 18.x or higher
- **pnpm** (recommended) or npm
- **Git**
- **PostgreSQL** 14+ (for production)

## Quick Setup

### 1. Clone the Repository

```bash
git clone https://github.com/hannie404/buoy-dashboard.git
cd buoy-dashboard
```

### 2. Install Dependencies

Using pnpm (recommended):
```bash
pnpm install --no-strict-peer-dependencies
```

Using npm:
```bash
npm install --legacy-peer-deps
```

### 3. Configure Environment Variables

Create a `.env.local` file in the root directory:

```bash
# Mapbox API Key
NEXT_PUBLIC_MAPBOX_TOKEN=your_mapbox_token_here

# OpenWeather API Key
NEXT_PUBLIC_OPENWEATHER_API_KEY=your_openweather_key_here

# Database (Optional for development)
DATABASE_URL=postgresql://user:password@localhost:5432/buoysense

# API Configuration (Optional)
API_BASE_URL=http://localhost:3001
```

#### Get API Keys

1. **Mapbox**: 
   - Visit [Mapbox Account](https://account.mapbox.com/)
   - Create a new access token
   - Copy your public token

2. **OpenWeather**:
   - Visit [OpenWeather API](https://openweathermap.org/api)
   - Sign up for a free account
   - Generate an API key

### 4. Run Development Server

```bash
pnpm dev
# or
npm run dev
```

The application will be available at [http://localhost:3000](http://localhost:3000)

## Production Deployment

### Using Vercel (Recommended)

1. **Install Vercel CLI**:
```bash
npm install -g vercel
```

2. **Deploy**:
```bash
vercel deploy
```

3. **Add Environment Variables** in Vercel Dashboard:
   - Go to Settings → Environment Variables
   - Add all variables from `.env.local`

### Using Docker

1. **Build Docker Image**:
```bash
docker build -t buoysense .
```

2. **Run Container**:
```bash
docker run -p 3000:3000 \
  -e NEXT_PUBLIC_MAPBOX_TOKEN=your_token \
  -e NEXT_PUBLIC_OPENWEATHER_API_KEY=your_key \
  buoysense
```

### Manual Deployment

1. **Build for Production**:
```bash
pnpm build
```

2. **Start Production Server**:
```bash
pnpm start
```

## Database Setup

### PostgreSQL Setup

1. **Create Database**:
```sql
CREATE DATABASE buoysense;
CREATE USER buoysense_user WITH PASSWORD 'your_password';
GRANT ALL PRIVILEGES ON DATABASE buoysense TO buoysense_user;
```

2. **Run Migrations**:
```bash
npm run migrate
```

3. **Seed Data** (optional):
```bash
npm run seed
```

## Hardware Setup

### LoRa Gateway Configuration

1. **Install LoRa Gateway Software**:
```bash
git clone https://github.com/Lora-net/lora_gateway.git
cd lora_gateway
make
```

2. **Configure Frequency**:
   - Edit `global_conf.json`
   - Set frequency to 915 MHz (US) or 868 MHz (EU)

3. **Start Gateway**:
```bash
./lora_pkt_fwd
```

### Buoy Sensor Setup

Each buoy requires:
- ESP32 or Arduino board
- HC-SR04 ultrasonic sensor
- MPU-6050 gyroscope
- LoRa module (SX1276)
- Solar panel (5W) + LiPo battery (3.7V)

Upload the Arduino sketch from `/hardware/buoy-firmware/`

## Troubleshooting

### Common Issues

**Port Already in Use**:
```bash
# Kill process on port 3000
lsof -ti:3000 | xargs kill -9
```

**Module Not Found**:
```bash
# Clear cache and reinstall
rm -rf node_modules pnpm-lock.yaml
pnpm install --no-strict-peer-dependencies
```

**Mapbox Not Loading**:
- Verify your `NEXT_PUBLIC_MAPBOX_TOKEN` is set correctly
- Check if token has proper permissions
- Ensure domain is whitelisted in Mapbox dashboard

**Build Errors**:
```bash
# Clear Next.js cache
rm -rf .next
pnpm build
```

## System Requirements

### Minimum Requirements
- CPU: 2 cores
- RAM: 4 GB
- Storage: 10 GB
- Network: 10 Mbps

### Recommended Requirements
- CPU: 4+ cores
- RAM: 8 GB
- Storage: 50 GB SSD
- Network: 50+ Mbps

## Next Steps

- Configure [API endpoints](./category/api-reference)
- Set up [LoRa network](./lora-configuration)
- Deploy [buoy sensors](./buoy-deployment)
- Configure [alerts](./alert-configuration)

Need help? Check our [FAQ](./faq) or [contact support](mailto:support@buoysense.com).
