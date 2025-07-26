# ⏰ MCP Time Server

**[中文版](./README_ZH.md)** | **English**

> A comprehensive MCP server for time zone management and time conversion

## 🎯 Overview

A Model Context Protocol (MCP) server that provides powerful time zone utilities including current time retrieval across different time zones and seamless time conversion between zones. Built with TypeScript for reliability and designed to work with any MCP-compatible client.

## ✨ Features

- 🌍 **Global Time Zones**: Get current time in any time zone worldwide
- 🔄 **Time Conversion**: Convert time between different time zones with precision
- ⚡ **Fast Performance**: Efficient time calculations using native JavaScript APIs
- 🔧 **TypeScript**: Full type safety with comprehensive error handling
- 🌐 **Multi-Platform**: Supports both local MCP clients and Cloudflare Workers
- 📡 **HTTP Support**: Additional HTTP and SSE endpoints for web integration
- 🎨 **User-Friendly**: Clear, formatted time output with time zone information

## 📦 Installation

```bash
npm install mcp-time-server
```

Or use directly with npx:

```bash
npx mcp-time-server
```

## 🔧 Configuration

### Claude Desktop

```json
{
  "mcpServers": {
    "time": {
      "command": "npx",
      "args": ["mcp-time-server"]
    }
  }
}
```

### Cursor IDE

```json
{
  "mcpServers": {
    "time": {
      "command": "npx",
      "args": ["mcp-time-server"]
    }
  }
}
```

### VS Code with GitHub Copilot

```json
{
  "mcp.servers": {
    "time": {
      "command": "npx",
      "args": ["mcp-time-server"],
      "transport": "stdio"
    }
  }
}
```

### Local Development

```json
{
  "mcpServers": {
    "time": {
      "command": "node",
      "args": ["path/to/mcp-time-server/dist/cli.js"]
    }
  }
}
```

## 🛠️ Available Tools

### `get_current_time`
Get the current time in a specified time zone.

**Parameters:**
- `timezone` (optional): Time zone identifier (e.g., "America/New_York", "Asia/Tokyo", "Europe/London")
  - Default: "UTC" if not specified
  - Supports all standard IANA time zone names

**Example Usage:**
```
"What time is it now in Tokyo?"
"Get current time in New York"
"Show me the current UTC time"
"What's the time in London right now?"
```

**Returns:**
- Formatted date and time in the specified time zone
- Time zone identifier for confirmation
- 24-hour format (HH:MM:SS)
- Full date (YYYY/MM/DD)

**Example Response:**
```
2025/7/26 14:30:45 (Asia/Tokyo)
```

### `convert_time`
Convert time between different time zones.

**Parameters:**
- `source_timezone` (required): Source time zone identifier
- `time` (required): Time to convert in HH:MM format (24-hour)
- `target_timezone` (required): Target time zone identifier

**Example Usage:**
```
"Convert 14:30 from Tokyo time to New York time"
"What is 09:00 London time in Los Angeles?"
"Convert 18:45 from UTC to Sydney time"
```

**Returns:**
- Original time with source time zone
- Converted time with target time zone
- Clear conversion statement

**Example Response:**
```
14:30 在 Asia/Tokyo 相当于 01:30 在 America/New_York
```

## 🎮 Usage Examples

### Global Business Coordination
```
"What time is it now in our offices in London, Tokyo, and San Francisco?"
"Convert our 10:00 AM meeting time from EST to all other office time zones"
```

### Travel Planning
```
"If it's 3:00 PM in Paris, what time is it in my destination city Bangkok?"
"Convert my flight departure time 08:30 from LAX timezone to arrival timezone in Dubai"
```

### Development and Operations
```
"Get current UTC time for logging"
"Convert server maintenance time 02:00 UTC to all regional offices"
```

### Scheduling and Coordination
```
"Convert 15:30 CET to Pacific Standard Time for our team call"
"What's 9:00 AM Monday in Sydney equivalent to in London?"
```

## 🌍 Supported Time Zones

This server supports all standard IANA time zone identifiers, including:

### Major Regions
- **Americas**: America/New_York, America/Los_Angeles, America/Chicago, America/Toronto
- **Europe**: Europe/London, Europe/Paris, Europe/Berlin, Europe/Rome
- **Asia**: Asia/Tokyo, Asia/Shanghai, Asia/Hong_Kong, Asia/Singapore
- **Australia**: Australia/Sydney, Australia/Melbourne, Australia/Perth
- **Others**: UTC, GMT, and all other IANA zones

### Common Examples
```
UTC                    # Coordinated Universal Time
America/New_York       # Eastern Time (US)
America/Los_Angeles    # Pacific Time (US)
Europe/London          # Greenwich Mean Time
Europe/Paris           # Central European Time
Asia/Tokyo             # Japan Standard Time
Asia/Shanghai          # China Standard Time
Australia/Sydney       # Australian Eastern Time
```

## 🏗️ Development

### Local Setup

```bash
# Clone the repository
git clone https://github.com/SzeMeng76/mcp-time-server.git
cd mcp-time-server

# Install dependencies
npm install

# Build the project
npm run build

# Start the server
npm start
```

### Project Structure

```
mcp-time-server/
├── src/
│   ├── index.ts          # Main MCP server implementation
│   └── cli.ts            # CLI and HTTP server setup
├── dist/                 # Compiled JavaScript files
├── package.json          # Dependencies and scripts
├── tsconfig.json         # TypeScript configuration
└── README.md            # Documentation
```

### Core Dependencies

- **@modelcontextprotocol/sdk**: Official MCP server framework
- **zod**: Runtime type validation and schema definition
- **http**: Node.js HTTP server for web endpoints

## 🔧 Technical Details

### Time Zone Handling
- Uses JavaScript's native `Intl.DateTimeFormat` API for accurate time zone conversions
- Supports all IANA time zone identifiers
- Handles daylight saving time transitions automatically
- Provides 24-hour format for consistency

### Time Conversion Algorithm
The time conversion process involves several steps to ensure accuracy:

1. **Parse Input Time**: Convert HH:MM string to numeric values
2. **Create Local Date**: Build a date object for the current day
3. **UTC Conversion**: Convert to UTC as an intermediate step
4. **Source Validation**: Verify the input time in the source time zone
5. **Adjustment**: Apply any necessary corrections for time zone differences
6. **Target Formatting**: Format the result in the target time zone

### Error Handling
- Comprehensive input validation for time formats
- Clear error messages for invalid time zone identifiers
- Graceful handling of edge cases and DST transitions
- Type-safe parameter processing with Zod schemas

### Multi-Platform Support
- **MCP Client**: Standard stdio transport for MCP compatibility
- **HTTP Server**: REST endpoints for web integration
- **SSE Support**: Server-Sent Events for real-time updates
- **Cloudflare Workers**: Cloud deployment support

## 🌐 HTTP Endpoints

When running as an HTTP server, additional endpoints are available:

### `/mcp`
- **Method**: GET
- **Description**: Server status and available tools
- **Response**: JSON with server information

### `/sse`
- **Method**: GET
- **Description**: Server-Sent Events endpoint
- **Response**: Event stream for real-time updates

## ⚠️ Important Notes

### Time Zone Accuracy
- All calculations use official IANA time zone data
- Daylight saving time transitions are handled automatically
- Results are accurate for current date calculations
- Historical time zone changes may not be reflected for past dates

### Input Format
- Time must be provided in 24-hour format (HH:MM)
- Leading zeros are not required (e.g., "9:30" or "09:30")
- Seconds are not supported in input but are shown in output

### Performance Considerations
- Time zone calculations are performed in real-time
- No caching is implemented for maximum accuracy
- Minimal memory footprint with efficient algorithms

## 🚀 Common Use Cases

### Business Operations
- **Global Teams**: Coordinate meetings across multiple time zones
- **Customer Support**: Convert support hours to customer local time
- **Release Management**: Schedule deployments across global infrastructure

### Travel and Logistics
- **Flight Planning**: Convert flight times between departure and arrival zones
- **Event Planning**: Schedule international events and webinars
- **Travel Itineraries**: Plan activities in destination time zones

### Development and DevOps
- **Log Analysis**: Convert UTC timestamps to local time zones
- **Monitoring**: Display alerts in appropriate regional time zones
- **Deployment**: Schedule maintenance windows across regions

### Personal Productivity
- **Calendar Management**: Convert appointment times for travel
- **Communication**: Find optimal meeting times across time zones
- **Planning**: Coordinate with international colleagues and friends

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature-name`
3. Make your changes with proper TypeScript types
4. Test with various time zones and edge cases
5. Ensure error handling works correctly
6. Submit a pull request with clear description

### Development Guidelines

- Maintain TypeScript strict mode compliance
- Add comprehensive error handling for new features
- Test with both common and obscure time zones
- Document any new parameters or return formats
- Consider daylight saving time edge cases

## 📄 License

MIT License - see [LICENSE](LICENSE) file for details.

## ⚖️ Data and Accuracy

- **Time Zone Data**: Uses browser/Node.js built-in IANA time zone database
- **Accuracy**: Calculations are accurate for current date and standard transitions
- **Updates**: Time zone data is updated with JavaScript runtime updates
- **Limitations**: Historical time zone changes may not be fully supported
- **Reliability**: Suitable for business and personal scheduling applications

## 🙏 Acknowledgments

- **IANA**: For maintaining the comprehensive time zone database
- **MCP Community**: For the standardized protocol
- **JavaScript Intl API**: For robust internationalization support
- **Contributors**: Everyone who helps improve this project

---

*Built for global coordination, scheduling, and time zone management* ⏰🌍
