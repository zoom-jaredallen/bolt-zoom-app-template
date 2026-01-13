# Zoom App Template

A starter template for building Zoom Marketplace Apps with React, TypeScript, and the Zoom Apps SDK.

## Features

- ✅ @zoom/appssdk pre-configured
- ✅ React + TypeScript + Vite
- ✅ Zoom SDK utilities and React hooks
- ✅ Light/dark theme support matching Zoom's design
- ✅ bolt.diy OAuth proxy integration
- ✅ Marketplace manifest template

## Quick Start

1. **Install dependencies:**
   ```bash
   npm install
   ```

2. **Set up environment:**
   ```bash
   cp .env.example .env.local
   # Edit .env.local with your Zoom App credentials
   ```

3. **Start development server:**
   ```bash
   npm run dev
   ```

## Creating a Zoom App

1. Go to [Zoom Marketplace](https://marketplace.zoom.us/develop/create)
2. Create a new "Zoom App" (not OAuth app)
3. Copy your Client ID to `.env.local`
4. Set the Home URL to your deployed app URL
5. Add redirect URL: `https://zoomvibes.j4red4llen.com/api/oauth/proxy/callback`
6. Select required scopes: `meeting:read`, `meeting:write`, `user:read`

## Project Structure

```
src/
├── lib/
│   └── zoom.ts           # Zoom SDK initialization utilities
├── hooks/
│   └── useZoom.ts        # React hook for Zoom SDK
├── components/
│   └── ZoomApp.tsx       # Main app component
├── App.tsx               # Entry component
├── App.css               # Zoom-themed styles
└── main.tsx              # React mount

public/
└── manifest.json         # Zoom Marketplace manifest template

.bolt/
└── prompt                # bolt.diy-specific rules
```

## Using the Zoom SDK

```typescript
import { useZoom } from './hooks/useZoom';

function MyComponent() {
  const { isReady, userContext, meetingContext, notify } = useZoom();

  if (!isReady) return <div>Loading...</div>;

  return (
    <div>
      <p>Welcome, {userContext?.screenName}!</p>
      <button onClick={() => notify('Hello!', 'Message from your app')}>
        Send Notification
      </button>
    </div>
  );
}
```

## OAuth Authentication

This template uses bolt.diy's OAuth proxy for development:

- OAuth Start: `https://zoomvibes.j4red4llen.com/api/oauth/proxy/start?provider=zoom`
- OAuth Callback: `https://zoomvibes.j4red4llen.com/api/oauth/proxy/callback`

For production, implement your own OAuth server and update the redirect URLs.

## Deployment

1. Build the app:
   ```bash
   npm run build
   ```

2. Deploy `dist/` to any static hosting (Vercel, Netlify, Cloudflare Pages)

3. Update your Zoom App's Home URL to your deployed URL

4. Submit your app for review in Zoom Marketplace

## Resources

- [Zoom Apps SDK Documentation](https://developers.zoom.us/docs/zoom-apps/)
- [Zoom Marketplace](https://marketplace.zoom.us/)
- [bolt.diy](https://github.com/stackblitz-labs/bolt.diy)

## License

MIT
