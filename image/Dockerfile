FROM python:3.14-slim

ENV PYTHONUNBUFFERED=1 \
    PYTHONDONTWRITEBYTECODE=1 \
    PIP_NO_CACHE_DIR=1 \
    PIP_DISABLE_PIP_VERSION_CHECK=1

LABEL org.opencontainers.image.source="https://github.com/clbsoldev/docker-host-statuspage" \
      org.opencontainers.image.description="Per-host Docker container status dashboard (PWA)" \
      org.opencontainers.image.licenses="MIT"

WORKDIR /app

RUN pip install --no-cache-dir docker==7.1.0

COPY app.py style.css ./

EXPOSE 8080

# No curl/wget in the slim image, so check the port directly.
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
    CMD python -c "import socket; socket.create_connection(('127.0.0.1', 8080), timeout=2).close()" || exit 1

CMD ["python", "app.py"]
