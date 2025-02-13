# HubSpot MCP Server

## Overview

A Model Context Protocol (MCP) server implementation that provides integration with HubSpot CRM. This server enables AI models to interact with HubSpot data and operations through a standardized interface.

For more information about the Model Context Protocol and how it works, see [Anthropic's MCP documentation](https://www.anthropic.com/news/model-context-protocol).

## Components

### Resources

The server exposes the following resources:

* `hubspot://contacts`: A dynamic resource that provides access to HubSpot contacts
* `hubspot://companies`: A dynamic resource that provides access to HubSpot companies

All resources auto-update as their respective objects are modified in HubSpot.

### Tools

The server offers several tools for managing HubSpot objects:

#### Contact Management Tools
* `get_contacts`
  * Retrieve contacts from HubSpot
  * No input required
  * Returns: Array of contact objects

* `create_contact`
  * Create a new contact in HubSpot
  * Input:
    * `email` (string): Contact's email address
    * `firstname` (string): Contact's first name
    * `lastname` (string): Contact's last name
    * `properties` (dict, optional): Additional contact properties

#### Company Management Tools
* `get_companies`
  * Retrieve companies from HubSpot
  * No input required
  * Returns: Array of company objects

* `create_company`
  * Create a new company in HubSpot
  * Input:
    * `name` (string): Company name
    * `domain` (string): Company domain
    * `properties` (dict, optional): Additional company properties

### Prompts

The server provides a demonstration prompt:

* `hubspot-demo`: Interactive prompt for HubSpot operations
  * Required arguments:
    * `operation` - The type of operation to perform (e.g., "create", "get")
    * `object_type` - The type of object to operate on (e.g., "contact", "company")
  * Guides users through HubSpot operations

## Setup

### Prerequisites

You'll need a HubSpot access token. You can obtain this by:
1. Creating a private app in your HubSpot account:
   Follow the [HubSpot Private Apps Guide](https://developers.hubspot.com/docs/guides/apps/private-apps/overview)
   - Go to your HubSpot account settings
   - Navigate to Integrations > Private Apps
   - Click "Create private app"
   - Fill in the basic information:
     - Name your app
     - Add description
     - Upload logo (optional)
   - Define required scopes:
     - crm.objects.contacts.read
     - crm.objects.contacts.write
     - crm.objects.companies.read
     - crm.objects.companies.write
   - Review and create the app
   - Copy the generated access token

Note: Keep your access token secure and never commit it to version control.

### Docker Installation

1. Build the Docker image:
```bash
docker build -t mcp-hubspot .
```

2. Run the container:
```bash
docker run \
  -e HUBSPOT_ACCESS_TOKEN=your_access_token_here \
  mcp-hubspot
```

## Usage with Claude Desktop

### Docker Usage
```json
{
  "mcpServers": {
    "hubspot": {
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "-e",
        "HUBSPOT_ACCESS_TOKEN=your_access_token_here",
        "mcp-hubspot"
      ]
    }
  }
}
```

## Development

To set up the development environment:

```bash
pip install -e .
```

## License

This project is licensed under the MIT License. 