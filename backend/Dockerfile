
FROM python:3.10-slim

# Install curl and other dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    curl \
    gcc \
    libpq-dev \
    && rm -rf /var/lib/apt/lists/*

# Install Poetry
RUN curl -sSL https://install.python-poetry.org | python3 -

# Add Poetry to PATH
ENV PATH="${PATH}:/root/.local/bin"

# Set working directory
WORKDIR /app

# Copy the rest of the application code
COPY . .

# Copy only the pyproject.toml and poetry.lock files
COPY pyproject.toml poetry.lock* ./

# Install dependencies using Poetry
RUN poetry install
#RUN pip install poetry

# Copy the rest of the application code
#COPY . .

# Make the prestart script executable
#RUN chmod +x ./prestart.sh
#RUN poetry run bash ./prestart.sh


# Expose port 8000 (assuming your backend server runs on this port)
EXPOSE 8000

# Command to run the backend server 
#CMD ["poetry", "run", "uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000", "--reload"]
CMD ["sh", "-c", "poetry run bash ./prestart.sh && poetry run uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload"]

