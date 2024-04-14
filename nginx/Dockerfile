FROM ubuntu:22.04

# Install packages
RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y libpam-krb5
RUN apt-get install -y nginx nginx-extras ca-certificates msktutil heimdal-clients libpam-heimdal

# Add Kerberos configuration
COPY ./krb5/krb5.conf /etc/krb5.conf
COPY ./krb5/nginx /etc/pam.d/nginx

# Add CA certificate
COPY ./certs/ca.crt /usr/local/share/ca-certificates/ca.crt
RUN update-ca-certificates

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]