# OpenCrMS - Verifiable Credentials Platform

An open source credential management system for issuing, managing, and verifying
digital credentials, with a focus on using the capabilities of the
[DIDComm](https://didcomm.org/) protocols for secure, private, and interoperable
exchange of verifiable credentials.

OpenCrMS is a project of [LF Decentralized Trust (LFDT)](https://www.lfdecentralizedtrust.org/)
and is run under the Maintainer Council governance model. See the
[OpenCrMS governance repository](https://github.com/OpenCrMS/governance) for details.

## Features

### Credential Management
- **Visual Credential Designer** - Drag-and-drop interface for designing credential cards with custom branding, images, and layouts
- **Schema Management** - Create and manage credential schemas with support for multiple DID methods (cheqd, did:web, did:key)
- **Credential Definitions** - Define credential types with OCA (Overlay Capture Architecture) branding overlays

### Issuance & Verification
- **OID4VCI** - OpenID for Verifiable Credential Issuance support
- **OID4VP** - OpenID for Verifiable Presentations for credential verification
- **DIDComm Connections** - Peer-to-peer secure messaging and credential exchange
- **mDL/mdoc Support** - ISO 18013-5 mobile driver's license credentials

### Additional Features
- **OpenBadges 3.0** - Issue and verify OBv3 credentials (Credly-compatible)
- **Workflow Engine** - Configurable credential issuance workflows
- **Group Messaging** - Secure group communication with MLS protocol
- **Digital Signing** - Document signing with verifiable credentials
- **Proof of Execution (POE)** - Zero-knowledge proof verification

## Architecture

```
├── frontend/          # Next.js 16 frontend application
├── backend/           # Express.js backend with Credo-ts agent (SSI framework)
├── packages/          # Shared workflow SDK packages
│   ├── workflow-client/
│   ├── workflow-react/
│   ├── workflow-ui-core/
│   └── workflow-backend-express/
└── docker-compose.yml # Docker deployment configuration
```

## Quick Start

### Prerequisites
- Docker and Docker Compose
- Node.js 20+ (for local development)

### Environment Setup

1. Copy the example environment file:
   ```bash
   cp .env.example .env
   ```

2. Configure required variables in `.env`:
   ```env
   # Required
   POSTGRES_PASSWORD=your-secure-password
   JWT_SECRET=your-jwt-secret-min-32-chars
   MAIN_WALLET_KEY=your-wallet-key

   # Optional - for full features
   REDIS_URL=redis://localhost:6379
   ```

### Running with Docker

```bash
# Start all services
docker-compose up -d

# Access the application
# Frontend: http://localhost:3000
# Backend API: http://localhost:3002
```

### Local Development

```bash
# Install dependencies
yarn install

# Start backend
cd backend && yarn dev

# Start frontend (new terminal)
cd frontend && yarn dev
```

## API Overview

### Authentication
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - User login

### Connections
- `GET /api/connections` - List connections
- `POST /api/connections/invitation` - Create invitation
- `POST /api/connections/receive-invitation` - Accept invitation

### Credentials
- `GET /api/credentials` - List credentials
- `POST /api/credentials/issue` - Issue credential

### Schemas & Definitions
- `GET /api/schemas` - List schemas
- `POST /api/schemas` - Create schema
- `GET /api/credential-definitions` - List definitions
- `POST /api/credential-definitions` - Create definition

### OID4VC
- `POST /api/oid4vci/offers` - Create credential offer
- `POST /api/oid4vp/authorization-requests` - Create verification request

### OpenBadges
- `POST /api/openbadges/credentials/issue` - Issue badge
- `POST /api/openbadges/credentials/verify` - Verify badge

## Credential Designer

The visual credential designer allows you to:
- Design credential card layouts with drag-and-drop
- Add text, images, and attribute placeholders
- Set background colors, gradients, and images
- Configure branding with logos and colors
- Export to OCA (Overlay Capture Architecture) format
- Generate thumbnail previews automatically

## Technology Stack

- **Frontend**: Next.js 16, React 19, Tailwind CSS, Craft.js
- **Backend**: Express.js, Credo-ts (SSI Framework)
- **Database**: PostgreSQL with Askar wallet storage
- **Cache**: Redis (optional, for horizontal scaling)
- **Protocols**: DIDComm v2, OID4VC, OpenBadges 3.0

## Governance & Community

OpenCrMS is governed under the Maintainer Council model. Governance documents live
in the [OpenCrMS governance repository](https://github.com/OpenCrMS/governance):

| Document | Purpose |
| -------- | ------- |
| [GOVERNANCE.md](https://github.com/OpenCrMS/governance/blob/main/GOVERNANCE.md) | How the project is run: values, the Maintainer Council, how maintainers are added and removed, meetings, voting, and amendments. |
| [MAINTAINERS.md](https://github.com/OpenCrMS/governance/blob/main/MAINTAINERS.md) | Current and emeritus maintainers, with their affiliations. |
| [CONTRIBUTING.md](https://github.com/OpenCrMS/governance/blob/main/CONTRIBUTING.md) | How to contribute, including the pull request process and DCO sign-off requirement. |
| [CODE_OF_CONDUCT.md](https://github.com/OpenCrMS/governance/blob/main/CODE_OF_CONDUCT.md) | The standards of behavior we hold ourselves to, following the LFDT Code of Conduct. |
| [SECURITY.md](https://github.com/OpenCrMS/governance/blob/main/SECURITY.md) | How to report a vulnerability and how the Security Response Team handles it. |
| [ADOPTERS.md](https://github.com/OpenCrMS/governance/blob/main/ADOPTERS.md) | Organizations using OpenCrMS. |

Everyone is welcome to participate. A good place to start is the
[contributing guide](https://github.com/OpenCrMS/governance/blob/main/CONTRIBUTING.md).

## License

Unless otherwise noted, the contents of this repository are released under the
[Apache License 2.0](./LICENSE).
