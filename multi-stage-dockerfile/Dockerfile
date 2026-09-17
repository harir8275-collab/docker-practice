# ==========================================
# STAGE 1: Download packages
# ==========================================
FROM python:3.11-slim AS builder

WORKDIR /build

COPY requirements.txt .

# Install packages into a local folder named "wheels"
RUN pip wheel --no-cache-dir --no-deps --wheel-dir /build/wheels -r requirements.txt


# ==========================================
# STAGE 2: Fresh and clean runtime
# ==========================================
FROM python:3.11-slim

WORKDIR /app

# Copy ONLY the downloaded packages from Stage 1
COPY --from=builder /build/wheels /app/wheels
COPY requirements.txt .

# Install the packages locally without using the internet
RUN pip install --no-cache /app/wheels/* && rm -rf /app/wheels

# Copy your Python application script
COPY app.py .

CMD ["python", "app.py"]

