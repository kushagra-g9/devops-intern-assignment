FROM python:3.12-slim-bookworm

# Install required system packages for curl and certificates
RUN apt-get update && apt-get install -y --no-install-recommends \
    curl \
    ca-certificates \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

# Download and install uv
RUN curl -LsSf https://astral.sh/uv/install.sh | sh

# Add uv to PATH
ENV PATH="/root/.local/bin/:$PATH"

# Set working directory
WORKDIR /app

# Copy application code
COPY . .


# Expose the Flask app port
EXPOSE 8002

# Run app using uv
CMD ["uv", "run", "app.py"]
