# EverArt Forge MCP for Cline

![EverArt Forge MCP](icon.svg)

An advanced Model Context Protocol (MCP) server for [Cline](https://github.com/cline/cline) that integrates with EverArt's AI models to generate both vector and raster images. This server provides powerful image generation capabilities with flexible storage options and format conversion.

## Features

- **Vector Graphics Generation**
  - Create SVG vector graphics using Recraft-Vector model
  - Automatic SVG optimization
  - Perfect for logos, icons, and scalable graphics

- **Raster Image Generation**
  - Support for PNG, JPEG, and WebP formats
  - Multiple AI models for different styles
  - High-quality image processing

- **Flexible Storage**
  - Custom output paths and filenames
  - Automatic directory creation
  - Format validation and extension handling
  - Web project integration

## Available Models

- **5000:FLUX1.1**: Standard quality, general-purpose image generation
- **9000:FLUX1.1-ultra**: Ultra high quality for detailed images
- **6000:SD3.5**: Stable Diffusion 3.5 for diverse styles
- **7000:Recraft-Real**: Photorealistic style
- **8000:Recraft-Vector**: Vector art style (SVG output)

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/nickbaumann98/everart-forge-mcp.git
   cd everart-forge-mcp
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Build the project:
   ```bash
   npm run build
   ```

4. Get your EverArt API key:
   - Sign up at [EverArt](https://everart.ai/) 
   - Navigate to your account settings
   - Create or copy your API key

5. Add the server to your Cline MCP settings file:

   **For VS Code Extension**:  
   Edit `~/Library/Application Support/Code/User/globalStorage/saoudrizwan.claude-dev/settings/cline_mcp_settings.json`:

   ```json
   {
     "mcpServers": {
       "everart-forge": {
         "command": "node",
         "args": ["/absolute/path/to/everart-forge-mcp/build/index.js"],
         "env": {
           "EVERART_API_KEY": "your_api_key_here"
         },
         "disabled": false,
         "autoApprove": []
       }
     }
   }
   ```

   **For Claude Desktop App**:  
   Edit `~/Library/Application Support/Claude/claude_desktop_config.json` (macOS) or appropriate location for your OS

6. Restart Cline to load the new MCP server

## VS Code & GitHub Copilot Agent Support

For one-click installation, click one of the install buttons below:

[![Install with NPX in VS Code](https://img.shields.io/badge/VS_Code-NPM-0098FF?style=flat-square&logo=visualstudiocode&logoColor=white)](h[ttps://insiders.vscode.dev/redirect/mcp/install?name=brave&inputs=%5B%7B%22type%22%3A%22promptString%22%2C%22id%22%3A%22apiKey%22%7D%5D&config=%7B%22command%22%3A%22npx%22%2C%22args%22%3A%5B%22-y%22%2C%22%40modelcontextprotocol%2Fserver-brave-search%22%5D%2C%22env%22%3A%7B%22BRAVE_API_KEY%22%3A%22%24%7Binput%3Abrave_api_key%7D%22%7D%7D](https://insiders.vscode.dev/redirect/mcp/install?name=everart-forge&config=%7B%22command%22%3A%22node%22%2C%22args%22%3A%5B%22%2Fabsolute%2Fpath%2Fto%2Feverart-forge-mcp%2Fbuild%2Findex.js%22%5D%2C%22env%22%3A%7B%22EVERART_API_KEY%22%3A%22%24%7Binput%3Aeverart_api_key%7D%22%7D%7D&inputs=%5B%7B%22type%22%3A%22promptString%22%2C%22id%22%3A%22everart_api_key%22%2C%22description%22%3A%22EverArt+API+Key%22%2C%22password%22%3Atrue%7D%5D)) [![Install with NPX in VS Code Insiders](https://img.shields.io/badge/VS_Code_Insiders-NPM-24bfa5?style=flat-square&logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect/mcp/install?name=everart-forge&config=%7B%22command%22%3A%22node%22%2C%22args%22%3A%5B%22%2Fabsolute%2Fpath%2Fto%2Feverart-forge-mcp%2Fbuild%2Findex.js%22%5D%2C%22env%22%3A%7B%22EVERART_API_KEY%22%3A%22%24%7Binput%3Aeverart_api_key%7D%22%7D%7D&inputs=%5B%7B%22type%22%3A%22promptString%22%2C%22id%22%3A%22everart_api_key%22%2C%22description%22%3A%22EverArt+API+Key%22%2C%22password%22%3Atrue%7D%5D&quality=insiders)


For manual installation, click the install buttons above or add the following to your User Settings (JSON) file in VS Code (press `Ctrl + Shift + P` and type `Preferences: Open User Settings (JSON)`):

```json
{
  "mcp": {
    "inputs": [
      {
        "type": "promptString",
        "id": "everart_api_key",
        "description": "EverArt API Key",
        "password": true
      }
    ],
    "servers": {
      "everart-forge": {
        "command": "node",
        "args": ["/absolute/path/to/everart-forge-mcp/build/index.js"],
        "env": {
          "EVERART_API_KEY": "${input:everart_api_key}"
        }
      }
    }
  }
}
```

Alternatively, add this configuration to `.vscode/mcp.json` in your workspace:

```json
{
  "inputs": [
    {
      "type": "promptString",
      "id": "everart_api_key",
      "description": "EverArt API Key",
      "password": true
    }
  ],
  "servers": {
    "everart-forge": {
      "command": "node",
      "args": ["/absolute/path/to/everart-forge-mcp/build/index.js"],
      "env": {
        "EVERART_API_KEY": "${input:everart_api_key}"
      }
    }
  }
}
```

## Usage Examples

Once configured, you can use Cline to generate images with prompts like:

- "Generate a minimalist tech logo in SVG format using the Recraft-Vector model"
- "Create a photorealistic landscape image with the FLUX1.1-ultra model"
- "Make me a vector icon for my project that represents artificial intelligence"
- "Generate a professional company logo as an SVG file and save it to my desktop"

### Tool Capabilities

The server provides these tools:

#### generate_image

Generate images with extensive customization options:

```
Parameters:
- prompt (required): Text description of desired image
- model: Model ID (5000:FLUX1.1, 9000:FLUX1.1-ultra, 6000:SD3.5, 7000:Recraft-Real, 8000:Recraft-Vector)
- format: Output format (svg, png, jpg, webp)
- output_path: Custom output path for the image
- web_project_path: Path to web project root for proper asset organization
- project_type: Web project type (react, vue, html, next, etc.)
- asset_path: Subdirectory within the web project assets
- image_count: Number of images to generate (1-10)
```

Notes:
- SVG format is only available with Recraft-Vector (8000) model
- Default format is "svg" for model 8000, "png" for others
- You can specify combined model IDs (e.g., "8000:Recraft-Vector")

#### list_images

List all previously generated images stored by the server.

#### view_image

Open a specific image in the default image viewer:

```
Parameters:
- filename: Name of the image file to view
```

## Troubleshooting

- **Error: Invalid model ID**: Make sure you're using one of the supported model IDs (5000, 6000, 7000, 8000, 9000)
- **Format not compatible with model**: SVG format is only available with Recraft-Vector (8000) model
- **Image not found**: Use the list_images tool to see available images
- **API authentication failed**: Check your EverArt API key
- **Images not appearing**: Check file permissions and paths

## License

MIT License - see LICENSE file for details.
