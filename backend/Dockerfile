# Використовуємо офіційний Rust образ
FROM rust:1.87-slim as builder

# Встановлюємо Solana CLI (beta)
RUN sh -c "$(curl -sSfL https://release.solana.com/beta/install)"
ENV PATH="/root/.local/share/solana/install/active_release/bin:${PATH}"


RUN apt-get update && apt-get install -y \
    pkg-config \
    libssl-dev \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

# Встановлюємо робочу директорію
WORKDIR /app

# Копіюємо всі необхідні файли для збірки
COPY backend/Cargo.toml ./backend/
COPY backend/src ./backend/src/

# Збираємо Rust бекенд
WORKDIR /app/backend
RUN cargo build --release

# Запускаємо бекенд
CMD ["./spp-backend"] 