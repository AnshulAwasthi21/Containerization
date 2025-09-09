# ---------- Stage 1: Build ----------
FROM python:3.11-slim AS builder

WORKDIR /app

# Install build dependencies (for compiling packages)
RUN apt-get update && apt-get install -y gcc python3-venv

# Copy requirements and install into venv
COPY requirements.txt .
RUN python -m venv /opt/venv && \
/opt/venv/bin/pip install --no-cache-dir -r requirements.txt

# ---------- Stage 2: Runtime ----------
FROM python:3.11-slim

WORKDIR /app

# Copy venv from builder
COPY --from=builder /opt/venv /opt/venv

# Update PATH so venv Python/pip is default
ENV PATH="/opt/venv/bin:$PATH"

# Copy the project code
COPY devops/ /app/

EXPOSE 8000

CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]


