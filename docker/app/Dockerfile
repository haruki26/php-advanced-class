FROM php:8.5-cli-bookworm

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=1000

ENV COMPOSER_ALLOW_SUPERUSER=1

RUN apt-get update && apt-get install -y --no-install-recommends \
    git \
    unzip \
    zip \
    curl \
    libzip-dev \
    libicu-dev \
    libonig-dev \
    libxml2-dev \
 && docker-php-ext-install -j"$(nproc)" \
    pdo_mysql \
    mbstring \
    xml \
    zip \
    intl \
 && rm -rf /var/lib/apt/lists/*

COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

RUN groupadd --gid "${USER_GID}" "${USERNAME}" \
 && useradd --uid "${USER_UID}" --gid "${USER_GID}" -m "${USERNAME}" \
 && mkdir -p /workspace \
 && chown -R "${USERNAME}:${USERNAME}" /workspace

WORKDIR /workspace
USER vscode
