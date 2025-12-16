# AIHF Remote Gateway

A lightweight gateway for executing AI-powered workflows at the edge. Connect up to [aihf.io](https://aihf.io) for managed orchestration and secured control plane. With aihf remote gateway workflow data remains within your own Cloudflare account boundary.

## Overview

AIHF Remote Gateway is a Cloudflare Worker-based runtime that enables:

- Secure workflow execution in isolated environments
- KV-based state synchronisation with upstream platforms
- Third-party workflow code execution from R2 storage
- Session token validation and management

This gateway is designed to run on Cloudflare Workers, providing low-latency execution at the edge while maintaining a secure connection to a central orchestration platform.

## Architecture

```
┌─────────────────────────────────────────┐
│                   Control Plane         │
│                     (aihf.io)           │
│                                         │
└──────────────────────┬──────────────────┘
                       │
                       │ Control Data Sync 
                       ▼
┌─────────────────────────────────────────────────────────┐
│                AIHF Remote Gateway                      │
│            (this project - open source)                 │
│                                                         │
│   ┌─────────────┐    ┌─────────────┐                   │
│   │    Sync     │    │  Workflow   │                   │
│   │ Receiver    │    │  Runtime    │                   │
│   └─────────────┘    └─────────────┘                   │
│          │                  │                          │
│          ▼                  ▼                          │
│   ┌─────────────────────────────────────┐              │
│   │          Local Data Stores          │              │
│   └─────────────────────────────────────┘              │
└─────────────────────────────────────────────────────────┘
```

## Quick Start

### Prerequisites

- Cloudflare account with Workers enabled
- Wrangler CLI installed (`npm install -g wrangler`)
- Node.js 18+

### Installation

```bash
# Clone the repository
git clone https://github.com/aihf/aihf-remote-gateway.git
cd aihf-remote-gateway

# Install dependencies
npm install

# Copy example configuration
cp wrangler.example.toml wrangler.toml
```

### Configuration

Edit `wrangler.toml` with your settings:

```toml
name = "aihf-remote-gateway"
main = "src/index.ts"
compatibility_date = "2024-01-01"

[vars]
UPSTREAM_PLATFORM = "https://aihf.io"  

```

### Deployment

```bash
# Development
wrangler dev

# Production
wrangler deploy
```

## Connecting to aihf.io 

The easiest way to use AIHF Remote Gateway is with [aihf.io](https://aihf.io), which provides:

- Workflow orchestration and scheduling
- Admin dashboard for monitoring and configuration, archival, workflow deployment and scoping
- Full Identity Access MAnagement for AIHF Entities
- Team management and access control
- Automatic KV synchronisation
- Support and SLA guarantees

Sign up at [aihf.io](https://aihf.io) to get your API credentials and connect your gateway in minutes.

## Security

- All sync operations require valid bearer tokens issued by the control plane
- Session tokens are validated against the upstream platform
- Workflow code is executed in isolated contexts
- No secrets are stored in the gateway - all sensitive config comes from the control plane

## Contributing

Contributions are welcome! Please read [CONTRIBUTING.md](CONTRIBUTING.md) before submitting PRs.

## License

MIT License - see [LICENSE](LICENSE) for details.

## Maintained By

[AIHF.IO](https://aihf.io)

---

**Want managed orchestration without the ops overhead?** Check out [aihf.io](https://aihf.io) →
