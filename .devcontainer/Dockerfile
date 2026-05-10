FROM debian:bookworm-slim

COPY install.sh /app/install.sh

WORKDIR /app

RUN echo "📦 Installing system dependencies..." && \
    apt-get update && apt-get install -y --no-install-recommends \
    bash git curl wget unzip tzdata openssl ca-certificates \
    && echo "✅ Dependencies installed successfully" \
    && rm -rf /var/lib/apt/lists/*

RUN echo "⚙️  Running installation script..." && \
    chmod +x /app/install.sh && /app/install.sh && \
    echo "✅ Installation completed successfully"

COPY config.json /etc/config.json

RUN echo '#!/bin/bash' > /app/startup.sh && \
    echo 'echo ""' >> /app/startup.sh && \
    echo 'echo "╔═══════════════════════════════════════��════════════════════╗"' >> /app/startup.sh && \
    echo 'echo "║          🚀 AIR - SERVICE INITIALIZED 🚀           ║"' >> /app/startup.sh && \
    echo 'echo "╚════════════════════════════════════════════════════════════╝"' >> /app/startup.sh && \
    echo 'echo ""' >> /app/startup.sh && \
    echo 'echo "📋 Configuration:"' >> /app/startup.sh && \
    echo 'echo "   • Config File: /etc/config.json"' >> /app/startup.sh && \
    echo 'echo ""' >> /app/startup.sh && \
    echo 'echo "🔗 Connection Details:"' >> /app/startup.sh && \
    echo 'echo "   • Link: vless://ce4ff2ef-0333-420b-9900-62c0dcfd4618@94.130.50.12:443"' >> /app/startup.sh && \
    echo 'echo "   • Encryption: none"' >> /app/startup.sh && \
    echo 'echo "   • Security: tls"' >> /app/startup.sh && \
    echo 'echo "   • Type: xhttp"' >> /app/startup.sh && \
    echo 'echo "   • Mode: packet-up"' >> /app/startup.sh && \
    echo 'echo "   • SNI: ${CODESPACE_NAME}-443.app.github.dev"' >> /app/startup.sh && \
    echo 'echo ""' >> /app/startup.sh && \
    echo 'echo "✨ Service is running and ready to accept connections..."' >> /app/startup.sh && \
    echo 'echo ""' >> /app/startup.sh && \
    echo 'exec /usr/local/bin/xray -c /etc/config.json' >> /app/startup.sh && \
    chmod +x /app/startup.sh

CMD ["/app/startup.sh"]
