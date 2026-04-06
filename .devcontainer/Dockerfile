FROM mcr.microsoft.com/devcontainers/base:jammy

RUN useradd -m -s /bin/bash ares \
    && mkdir -p /var/www/html \
    && chown ares:ares /var/www/html \
    && echo "ares ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/ares \
    && chmod 0440 /etc/sudoers.d/ares
