# Topstep, Apex and Tradovate Auto Trader Extension

A professional Chrome extension for automated trading on the Tradovate platform. This extension connects to a WebSocket server to receive trading signals and automatically executes trades.

## Features

- 🔄 **Auto-Reconnect**: Automatically reconnects if connection drops
- 📊 **Real-time Status Monitoring**: Live connection status with uptime tracking
- 💓 **Heartbeat/Keep-Alive**: Maintains stable connection with server
- ⚙️ **Configurable Settings**: Customize WebSocket URL, token, and reconnect behavior
- 🛡️ **Error Handling**: Graceful error recovery and clear status reporting
- 📈 **Signal Counter**: Tracks total signals received

# Topstep, Apex and Tradovate Auto Trader - Installation & Setup Guide

## Installation

1. **Download** the `tradovate_extension.crx` file

2. **Open Chrome** and go to: `chrome://extensions/`

3. **Enable Developer Mode** - Toggle switch in top right corner

4. **Drag and drop** the `.crx` file onto the extensions page

5. **Click "Add extension"** when prompted

## Configuration

1. **Open Tradovate** - Go to `https://topstep.tradovate.com` , `https://apex.tradovate.com`  `https://trader.tradovate.com`

2. **Click Extension Icon** - The "T" icon in Chrome toolbar

3. **Configure Token** (if needed):
   - Click "Configuration" button
   - Change Token from default "topstep" to your token
   - Click "Save Configuration"

## TradingView Alert Setup

### 1. Create Alert in TradingView
- Right-click on chart → "Add Alert" 
- Or use Alt+A (Windows) / Option+A (Mac)

### 2. Configure Alert Settings
- **Condition**: Your trading strategy/indicator
- **Alert name**: "Buy Signal" or "Sell Signal"

### 3. Set Webhook URL
- Check "Webhook URL" option
- Enter your server webhook URL that forwards to WebSocket

### 4. Set Alert Message (JSON Format)

For **BUY** signals:
```json
{ "type": "buy", "userName": "topstepdemo" }
```

For **SELL** signals:
```json
{ "type": "sell", "userName": "topstepdemo" }
```

For **EXIT** positions:
```json
{ "type": "exit-mkt-cxl", "userName": "topstepdemo" }
```

### 5. Important Settings
- **Expiration**: Set to "Open-ended" for permanent alerts
- **Alert actions**: Choose when to trigger (Once Per Bar, Once Per Bar Close, etc.)

## How It Works

1. TradingView triggers alert based on your conditions
2. Alert sends JSON message to your webhook server
3. Webhook server forwards signal through WebSocket
4. Extension receives signal and clicks corresponding button on Tradovate

## Testing

1. Connect extension to server (green status)
2. Create a test alert in TradingView
3. Manually trigger it 
4. Watch the Tradovate platform for automatic button clicks

## Token Configuration

The token is used to identify different users/accounts:

- **Default**: `topstep`
- **Change to**: Your token
- **Format**: Letters and numbers only, no spaces
- **Example**: `user123`, `myaccount`, `trader1`

Server must validate: `userName` in JSON must match configured token



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
