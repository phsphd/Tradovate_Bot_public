# Topstep, Apex and Tradovate Auto Trader Extension

A professional Chrome extension for automated trading on the Tradovate platform. This extension connects to a WebSocket server to receive trading signals and automatically executes trades.

## Features

- 🔄 **Auto-Reconnect**: Automatically reconnects if connection drops
- 📊 **Real-time Status Monitoring**: Live connection status with uptime tracking
- 💓 **Heartbeat/Keep-Alive**: Maintains stable connection with server
- ⚙️ **Configurable Settings**: Customize WebSocket URL, token, and reconnect behavior
- 🛡️ **Error Handling**: Graceful error recovery and clear status reporting
- 📈 **Signal Counter**: Tracks total signals received

## Installation

### Method 1: Load Unpacked (Development)

1. Download or clone this repository
2. Open Chrome and navigate to `chrome://extensions/`
3. Enable "Developer mode" (toggle in top right)
4. Click "Load unpacked"
5. Select the extension folder containing `manifest.json`

### Method 2: Install from .crx (Distribution)

1. Download the `.crx` file
2. Open Chrome and navigate to `chrome://extensions/`
3. Drag and drop the `.crx` file onto the page
4. Click "Add extension" when prompted

## Usage

### Initial Setup

1. Navigate to any Tradovate platform URL (e.g., `topstep.tradovate.com` or `trader.tradovate.com`)
2. Click the extension icon in Chrome toolbar
3. (Optional) Click "Configuration" to customize settings:
   - **WebSocket URL**: Default `wss://excellgen.com/websk/`
   - **Token**: Default `topstep`
   - **Reconnect Delay**: Time in seconds between reconnection attempts
   - **Auto-reconnect**: Enable/disable automatic reconnection

### Connecting

1. Click "Connect to Server" button
2. Status indicator will show:
   - 🔴 Red = Disconnected
   - 🟡 Yellow = Connecting
   - 🟢 Green = Connected
3. Once connected, the extension will display uptime and signal count

### Trading Signals

The extension responds to the following WebSocket commands:

| Command | Action | Example |
|---------|--------|---------|
| `buy` | Clicks "Buy Mkt" button | `{"type": "buy"}` |
| `sell` | Clicks "Sell Mkt" button | `{"type": "sell"}` |
| `exit-mkt-cxl` | Clicks "Exit at Mkt & Cxl" button | `{"type": "exit-mkt-cxl"}` |
| `cancel-all` | Clicks "Cancel All" button | `{"type": "cancel-all"}` |

### Monitoring

- **Status Box**: Shows current connection state and details
- **Uptime**: Displays connection duration (MM:SS format)
- **Signals**: Counter showing total signals received
- **Console Logs**: Open browser console (F12) to see detailed activity logs

## Configuration

### Saving Settings

1. Click "Configuration" button
2. Modify desired settings
3. Click "Save Configuration"
4. Settings persist across browser sessions

### WebSocket Server Requirements

Your WebSocket server should:
- Accept connections at the configured URL with token parameter
- Send JSON messages with a `type` field
- Respond to `ping` messages with `pong` (optional but recommended)

## Troubleshooting

### Extension Not Working

1. **Check URL**: Ensure you're on a Tradovate platform URL
2. **Reload Page**: Refresh the trading platform page
3. **Re-inject**: Disconnect and reconnect the extension
4. **Check Console**: Press F12 and look for error messages

### Connection Issues

- **Status shows "Not on Tradovate platform"**: Navigate to a valid Tradovate URL
- **Connection drops frequently**: Check your internet connection and WebSocket server
- **Auto-reconnect not working**: Verify it's enabled in configuration

### Buttons Not Clicking

- Open browser console (F12) to see which buttons the extension finds
- Ensure the trading interface is fully loaded
- Check that button text matches exactly (e.g., "Buy Mkt", "Sell Mkt")

## Development

### File Structure

```
topstep-auto-trader/
├── manifest.json      # Extension manifest
├── popup.html         # Popup interface
├── popup.js          # Popup logic and WebSocket management
├── icon.svg          # Extension icon
└── README.md         # This file
```

### Building for Distribution

1. Make your changes
2. Test thoroughly
3. Go to `chrome://extensions/`
4. Click "Pack extension"
5. Select the extension directory
6. Chrome creates `.crx` and `.pem` files

### WebSocket Protocol

The extension expects JSON messages:
```json
{
  "type": "buy|sell|exit-mkt-cxl|cancel-all",
  "userName": "optional-field"
}
```

Server should handle:
- Initial connection message: `"browser client connected"`
- Heartbeat: `{"type": "ping"}` → respond with `{"type": "pong"}`

## Security Considerations

- Only connects to configured WebSocket URL
- Token-based authentication (configure your own secure token)
- No sensitive data stored locally
- All trades require active browser tab

## Support

For issues or questions:
1. Check browser console for detailed error messages
2. Verify WebSocket server is running and accessible
3. Ensure trading platform interface hasn't changed

## License

This extension is provided as-is for educational and personal use. Always follow your broker's terms of service and trade responsibly.

---

**Version**: 2.0  
**Last Updated**: June 2025
