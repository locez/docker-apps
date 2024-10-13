# Caddy Reverse Proxy for JX3App

This project sets up a reverse proxy using Caddy to forward requests to `https://m.pvp.xoyo.com` while handling CORS (Cross-Origin Resource Sharing) preflight requests. The configuration also includes HTTPS support using custom certificates.

## Table of Contents

- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Configuration](#configuration)
- [Usage](#usage)
- [Docker Setup](#docker-setup)
- [CORS Handling](#cors-handling)
- [HTTPS Configuration](#https-configuration)
- [Contributing](#contributing)
- [License](#license)

## Overview

The Caddy server is configured to listen on port `44443` for both HTTP and HTTPS traffic. It acts as a reverse proxy for `https://m.pvp.xoyo.com`, ensuring that the `Host` header is correctly forwarded. Additionally, it handles CORS preflight requests to allow cross-origin requests from any origin.

## Prerequisites

- Docker
- Docker Compose
- Custom SSL certificates for `jx3app.proxy.locez.com`

## Configuration

### Caddyfile

The `Caddyfile` is the main configuration file for Caddy. It includes the following settings:

- **Ports**: Listens on port `80` for HTTP and `44443` for HTTPS.
- **Reverse Proxy**: Forwards requests to `https://m.pvp.xoyo.com` and sets the `Host` header to the upstream host and port.
- **CORS Preflight**: Handles `OPTIONS` requests for CORS preflight checks, allowing requests from any origin with specific headers and methods.
- **HTTPS**: Uses custom SSL certificates located at `/etc/certs/jx3app.proxy.locez.com.pem` and `/etc/certs/jx3app.proxy.locez.com.key`.

### Docker Compose

The `docker-compose.yml` file sets up the Caddy service with the following configurations:

- **Image**: Uses the official Caddy Docker image.
- **Ports**: Maps ports `443` and `44443` to the host.
- **Volumes**: Mounts the `certs` directory, `Caddyfile`, and data volumes for persistent storage.

## Usage

1. **Clone the Repository**:
   ```bash
   git clone <repository-url>
   cd <repository-directory>
   ```

2. **Place Certificates**:
   Ensure that your SSL certificates are placed in the `certs` directory.

3. **Start the Service**:
   ```bash
   docker-compose up -d
   ```

4. **Access the Service**:
   Access the service via `https://jx3app.proxy.locez.com:44443`.

## Docker Setup

The Docker setup is managed using Docker Compose. The `docker-compose.yml` file defines the Caddy service and its dependencies.

### Volumes

- `caddy-reverse-jx3app_caddy_data`: Persistent data storage for Caddy.
- `caddy_config`: Configuration storage for Caddy.

## CORS Handling

CORS preflight requests are handled by responding with a `204 No Content` status and setting the necessary CORS headers. This allows any origin to make requests to the server.

## HTTPS Configuration

The HTTPS configuration uses custom SSL certificates located in the `certs` directory. Ensure that these certificates are valid and correctly named.

## Contributing

Contributions are welcome! Please feel free to submit a pull request or open an issue for any improvements or bug fixes.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

Feel free to customize this README further based on your specific needs or additional details you'd like to include.
