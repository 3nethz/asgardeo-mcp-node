# @brionmario-experimental/mcp-node

[![npm version](https://img.shields.io/npm/v/@brionmario-experimental/mcp-node.svg?style=flat-square)](https://www.npmjs.com/package/@brionmario-experimental/mcp-node)
[![npm downloads](https://img.shields.io/npm/dm/@brionmario-experimental/mcp-node.svg?style=flat-square)](https://www.npmjs.com/package/@brionmario-experimental/mcp-node)

Node.js core library for enforcing Model Context Protocol (MCP) authorization using Asgardeo.

## Overview

This package provides the core functionality for implementing Model Context Protocol (MCP) based authorization in
Node.js applications. It serves as the foundation for higher-level implementations like the Express middleware
(`@brionmario-experimental/mcp-express`).

This package is part of the
[Asgardeo MCP Node.js SDKs monorepo](https://github.com/brionmario/asgardeo-mcp-node#readme). For overall project
information, contribution guidelines, and details on other related packages, please refer to the main repository.

## Installation

```bash
npm install @brionmario-experimental/mcp-node
# or
yarn add @brionmario-experimental/mcp-node
# or
pnpm add @brionmario-experimental/mcp-node
```

## Features

- Authorization server metadata generation
- Protected resource metadata generation
- Token verification utilities

## Usage

```typescript
import {
  generateAuthorizationServerMetadata,
  generateProtectedResourceMetadata,
} from '@brionmario-experimental/mcp-node';

baseUrl: string = 'https://api.asgardeo.io/<your-org-name>';

// Generate authorization server metadata
const serverMetadata = generateAuthorizationServerMetadata({
  baseUrl,
});

// Generate protected resource metadata
const resourceMetadata = generateProtectedResourceMetadata({
  authorizationServers: [baseUrl],
  resource: 'https://api.example.com',
});
```

## API Reference

### Metadata Generation

#### generateAuthorizationServerMetadata(options)

Generates metadata for the authorization server.

```typescript
const metadata = generateAuthorizationServerMetadata({
  baseUrl: 'https://api.asgardeo.io',
});
```

#### generateProtectedResourceMetadata(options)

Generates metadata for protected resources.

```typescript
const metadata = generateProtectedResourceMetadata({
  authorizationServers: ['https://api.asgardeo.io'],
  resource: 'https://api.example.com',
});
```

### Configuration

#### McpAuthOptions

Configuration options used across MCP packages.

```typescript
interface McpAuthOptions {
  /** Base URL of the authorization server */
  baseUrl: string;
  /** Optional audience value for token validation */
  audience?: string;
}
```

### Token Verification

#### validateToken(accessToken, jwksUri, options)

Verifies a JWT access token using the authorization server's JWKS endpoint.

```typescript
import {validateToken} from '@brionmario-experimental/mcp-node';

await validateToken('<token>', 'https://api.asgardeo.io/oauth2/jwks', {
  issuer: 'https://api.asgardeo.io/oauth2/token',
  audience: 'mcp-client-id',
  clockTolerance: 60,
});
```

### Prerequisites

- Node.js 16.x or later
- pnpm 8.x or later

### Setup

1. Clone the repository
2. Install dependencies:

```bash
pnpm install
```

### Build

```bash
pnpm build
```

### Lint

```bash
pnpm lint
```

## License

Apache-2.0 - see the [LICENSE](LICENSE) file for details.
