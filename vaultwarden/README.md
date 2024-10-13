# Caddy Docker Configuration for Vaultwarden

This repository contains a Docker Compose setup for running [Vaultwarden](https://github.com/dani-garcia/vaultwarden) (an unofficial Bitwarden server implementation) behind a [Caddy](https://caddyserver.com/) reverse proxy. The setup includes automatic HTTPS certificate management using the ACME DNS-01 challenge with Aliyun DNS.

## Features

- **Automatic HTTPS**: Caddy automatically manages SSL certificates using the ACME DNS-01 challenge with Aliyun DNS.
- **Reverse Proxy**: Caddy acts as a reverse proxy for Vaultwarden, ensuring secure communication over HTTPS.
- **Logging**: Access logs are stored in a specified file with rolling capabilities.
- **Environment Variables**: Configuration is driven by environment variables, making it easy to customize the setup.

## Prerequisites

- Docker and Docker Compose installed on your server.
- An Aliyun account with API access keys for DNS management.
- A domain name pointing to your server.

## Configuration

### Environment Variables

Before running the setup, you need to configure the following environment variables:

- `DOMAIN`: The domain name for your Vaultwarden instance (e.g., `https://example.locez.com`).
- `LOG_FILE`: The path to the access log file (e.g., `access.log`).
- `EMAIL`: The email address to use for ACME registration.
- `ALIYUN_ACCESS_KEY_ID`: Your Aliyun access key ID for DNS management.
- `ALIYUN_ACCESS_KEY_SECRET`: Your Aliyun access key secret for DNS management.

### Caddyfile

The `Caddyfile` is configured to:

- Log access requests to a specified file with rolling capabilities.
- Use the ACME DNS-01 challenge to obtain SSL certificates for the configured domain.
- Proxy all requests to the Vaultwarden service.

### Docker Compose

The `docker-compose.yml` file defines two services:

- **vaultwarden**: Runs the Vaultwarden server.
- **caddy**: Runs the Caddy server with the specified configuration.

## Usage

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/locez/docker-apps.git
   cd docker-apps/vaultwarden
   ```

2. **Set Environment Variables**:
   Create a `.env` file in the root directory with the following content:
   ```env
   DOMAIN=https://example.locez.com
   LOG_FILE=access.log
   EMAIL=locez@locez.com
   ALIYUN_ACCESS_KEY_ID=your_aliyun_access_key_id
   ALIYUN_ACCESS_KEY_SECRET=your_aliyun_access_key_secret
   ```

3. **Start the Services**:
   ```bash
   docker-compose up -d
   ```

4. **Access Vaultwarden**:
   Open your browser and navigate to `https://example.locez.com`.

## Customization

- **Caddyfile**: Modify the `Caddyfile` to change logging settings, reverse proxy behavior, or add additional Caddy features.
- **Environment Variables**: Adjust the environment variables in the `.env` file to match your specific configuration.

## Troubleshooting

- **Certificate Issues**: Ensure that your Aliyun DNS is correctly configured and that the domain is pointing to your server.
- **Log Files**: Check the `access.log` file for any errors or warnings.
- **Proxy Issues**: If you encounter issues with the reverse proxy, try disabling the `encode gzip` directive in the `Caddyfile`.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Acknowledgments

- [Vaultwarden](https://github.com/dani-garcia/vaultwarden) for the Bitwarden server implementation.
- [Caddy](https://caddyserver.com/) for the powerful and easy-to-use web server.
- [Aliyun](https://www.aliyun.com/) for DNS management services.

---

Feel free to contribute or report issues!