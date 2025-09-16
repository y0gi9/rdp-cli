# RDP Connection Manager

A bash-based interactive CLI tool for managing FreeRDP connections with an intuitive menu-driven interface.

## Features

- Interactive menu navigation with arrow keys
- Save and manage multiple RDP connection profiles
- Support for various resolution modes:
  - Fullscreen
  - Responsive (dynamic scaling)
  - Smart fullscreen
  - Custom resolutions
- Performance optimization options
- Multi-monitor support detection
- Clipboard isolation by default with optional text-only sharing (file clipboard stays disabled for stability)
- Clipboard direction controls available when host sharing is explicitly enabled
- Color depth settings (8, 15, 16, 24, 32 bits)
- Audio redirection options
- JSON-based configuration storage

## Prerequisites

- FreeRDP client (`freerdp`)
- `jq` for JSON processing
- `xrandr` for display detection (optional)
- `hyprctl` for Hyprland window detection (optional)

## Installation

1. Make the script executable:
   ```bash
   chmod +x rdp-manager
   ```

2. Optionally, move to a directory in your PATH:
   ```bash
   sudo mv rdp-manager /usr/local/bin/
   ```

3. Keep `freerdp-safe` alongside `rdp-manager` or install it in your `PATH`. The manager now locates the wrapper automatically, including when launched through an alias.

## Usage

Run the script:
```bash
./rdp-manager
```

### Optional alias

Place both `rdp-manager` and `freerdp-safe` in the same directory (or install them system-wide) and add an alias such as:

```bash
alias rdp='rdp-manager'
```

The manager resolves the wrapper relative to the script, so the alias works from any working directory.

### Main Menu Options

1. **Connect to saved RDP instance** - Select and connect to a previously configured connection
2. **Add new RDP connection** - Create a new connection profile
3. **Edit existing connection** - Modify an existing connection profile
4. **Delete connection** - Remove a connection profile
5. **List all connections** - Display all saved connections
6. **Exit** - Quit the application

### Navigation

- Use arrow keys (↑/↓) to navigate menu options
- Press Enter to select an option
- Use number keys (1-6) for quick selection

## Configuration

Connection profiles are stored in `~/.config/rdp-manager/connections.json` in JSON format.

### Example Connection Profile

```json
{
  "name": "Windows Server",
  "host": "192.168.1.100",
  "port": "3389",
  "username": "Administrator",
  "password": "encrypted_password",
  "domain": "MYDOMAIN",
  "resolution": "1920x1080",
  "color_depth": "32",
  "sound": "true",
  "clipboard": "true",
  "clipboard_mode": "remote-to-local",
  "drives": "false",
  "perf_mode": "true"
}
```

## Security Features

- Uses `freerdp-safe` wrapper for enhanced security
- Ignores certificate warnings (configurable)
- TLS encryption by default
- Password encryption in configuration files

## Resolution Modes

- **Fullscreen**: Opens RDP in fullscreen mode
- **Responsive**: Dynamic window sizing that adapts to your current window
- **Smart Fullscreen**: Fullscreen with dynamic resolution adjustment
- **Custom**: Fixed resolution with smart scaling

## Performance Options

When performance mode is enabled:
- LAN network optimization
- Disabled wallpaper
- Disabled menu animations

## Troubleshooting

- Ensure FreeRDP is installed and accessible
- Check that the target RDP server is reachable
- Verify credentials and network connectivity
- For display issues, ensure xrandr is available
- Clipboard sharing is opt-in. By default the remote session keeps its own clipboard so host applications remain stable. When editing a connection you can enable text clipboard sync and pick the direction if you accept the risk.

## License

This project is open source and available under standard terms.
# rdp-cli
# rdp-cli
