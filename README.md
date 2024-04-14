# Nginx Proxy

## Description

Proxy server for monitoring services. This server use Kerberos for authentication.

## Installation

```bash
docker-compose up -d
```

## Update

```bash
docker-compose up --force-recreate --build -d
```

## Remove

```bash
docker-compose down
```

## Ports

- 80 - http redirect to https
- 443 - https

## SSL certificates

For work with SSL certificates you need to create files:

- `nginx/certs/cert.crt`
- `nginx/certs/key.key`
- `nginx/certs/ca.pem`

## Nginx configuration

Configuration web server in `nginx/config/nginx.conf`. In this file set proxy server settings.

## Kerberos

This proxy server use Kerberos for authentication. For work need files:

- `nginx/krb5/krb5.conf`
- `nginx/krb5/nginx`

If you don't have Kerberos server, you can delete this files and remove Kerberos settings from `nginx/config/default`:

```conf
        # Remove this strings
        auth_pam "Kerberos Authentication";
        auth_pam_service_name "nginx";
```

Remove copy files from `Dockerfile`:

```conf
# Remove this strings
COPY ./krb5/krb5.conf /etc/krb5.conf
COPY ./krb5/nginx /etc/pam.d/nginx
```
