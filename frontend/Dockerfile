FROM python:3.9-slim

WORKDIR /app

# Install system dependencies
RUN apt-get update && apt-get install -y \
    gcc \
    python3-dev \
    && rm -rf /var/lib/apt/lists/*

# Install Python dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy application code
COPY . .

# Create .env file from build arguments
ARG STREAMLIT_SERVER_PORT
ARG STREAMLIT_SERVER_HEADLESS
RUN echo "STREAMLIT_SERVER_PORT=$STREAMLIT_SERVER_PORT" > .env
RUN echo "STREAMLIT_SERVER_HEADLESS=$STREAMLIT_SERVER_HEADLESS" >> .env

# Environment variables
ENV STREAMLIT_SERVER_PORT=$STREAMLIT_SERVER_PORT
ENV STREAMLIT_SERVER_HEADLESS=$STREAMLIT_SERVER_HEADLESS

EXPOSE 8501

CMD ["streamlit", "run", "frontend.py", "--server.port=8501", "--server.address=0.0.0.0"]