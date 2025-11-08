# BuoySense Documentation

Official documentation for the BuoySense IoT Flood Monitoring System, built with [Docusaurus](https://docusaurus.io/).

## 🌐 Live Documentation

- **Production**: https://docs-buoysense.yourdomain.com
- **Staging**: https://buoy-sense-docs.vercel.app

## Installation

```bash
npm install
```

## Local Development

```bash
npm start
```

This command starts a local development server and opens up a browser window. Most changes are reflected live without having to restart the server.

## Build

```bash
npm build
```

This command generates static content into the `build` directory and can be served using any static contents hosting service.

## Deployment

### Deploy to Vercel (Recommended)

1. Install Vercel CLI: `npm install -g vercel`
2. Deploy: `vercel deploy --prod`
3. Set up custom domain: `docs-buoysense.yourdomain.com`

### Deploy to GitHub Pages

```bash
GIT_USER=<Your GitHub username> npm deploy
```

If you are using GitHub pages for hosting, this command is a convenient way to build the website and push to the `gh-pages` branch.

## Links

- Main Dashboard: [github.com/hannie404/buoy-dashboard](https://github.com/hannie404/buoy-dashboard)
- Documentation Repo: [github.com/hannie404/buoy-sense-docs](https://github.com/hannie404/buoy-sense-docs)

