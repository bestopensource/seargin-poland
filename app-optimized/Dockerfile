# Etap 1: Budowanie środowiska
FROM python:3.8-slim AS builder

# Ustawienie zmiennych środowiskowych dla bezpieczeństwa i lepszej wydajności
ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

# Instalacja zależności systemowych potrzebnych tylko do budowy (z możliwością ich usunięcia po zakończeniu)
RUN apt-get update && apt-get install -y --no-install-recommends \
    gcc \
    libpq-dev \
    && rm -rf /var/lib/apt/lists/*

# Ustawienie katalogu roboczego
WORKDIR /app

# Kopiowanie plików aplikacji i zależności
COPY requirements.txt .

# Instalacja zależności aplikacji w izolowanym środowisku (np. w folderze build)
RUN pip install --user --no-cache-dir -r requirements.txt

# Etap 2: Tworzenie finalnego obrazu
FROM python:3.8-slim

ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

# Instalacja niezbędnych pakietów
RUN apt-get update && apt-get install -y --no-install-recommends \
    curl \
    && rm -rf /var/lib/apt/lists/*

# Ustawienie katalogu roboczego
WORKDIR /app

# Kopiowanie plików aplikacji
COPY . /app

# Kopiowanie zainstalowanych pakietów Pythona z etapu budowania
COPY --from=builder /root/.local /root/.local

# Ustawienie ścieżki dla zainstalowanych pakietów
ENV PATH=/root/.local/bin:$PATH

# Definicja domyślnej komendy uruchomienia aplikacji
CMD ["python", "app.py"]
