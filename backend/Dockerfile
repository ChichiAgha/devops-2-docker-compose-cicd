# # # Use official Python slim image
# # FROM python:3.10-slim

# # # Metadata
# # LABEL maintainer="DevOps Team"
# # LABEL description="Backend app built with Poetry and PostgreSQL support"

# # # Set workdir and copy project files
# # WORKDIR /app

# # # Install system dependencies (build tools, PostgreSQL libs, etc.)
# # RUN apt-get update && apt-get install -y --no-install-recommends \
# #     build-essential \
# #     libpq-dev \
# #     curl \
# #     && rm -rf /var/lib/apt/lists/*


# # RUN curl -sSL https://install.python-poetry.org | python3 - 

# # # Install Poetry
# # #ENV POETRY_VERSION=1.8.2

# # ENV PATH="/root/.local/bin:$PATH"


# # # Copy only dependency files first (for Docker layer caching)
# # COPY pyproject.toml poetry.lock* ./

# # # Copy the rest of the application
# # COPY . .


# # # Configure Poetry to not create virtualenvs
# # #ENV POETRY_VIRTUALENVS_CREATE=false

# # # Install Python dependencies
# # RUN poetry install --no-root --no-interaction --no-ansi

# # RUN chmod +x ./prestart.sh

# # #RUN poetry run bash ./prestart.sh


# # # Expose app port (adjust based on your framework)
# # EXPOSE 8000

# # # Default command (adjust for FastAPI/Django/etc.)
# # CMD ["sh", "-c", "poetry run bash ./prestart.sh && poetry run uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload"]


# # # pro tip
# # # ARG ENV=prod
# # # ENV ENV=${ENV}

# # # CMD ["sh", "-c", "if [ \"$ENV\" = \"dev\" ]; then poetry run bash ./prestart.sh && poetry run uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload; else poetry run uvicorn app.main:app --host 0.0.0.0 --port 8000; fi"]

# # ###t run 
# # ###docker build -t backend --build-arg ENV=dev .


# # Use Python 3.10 image as base
# FROM python:3.10

# # Set the working directory in the container
# WORKDIR /app

# # Install curl and bash
# RUN apt-get update -y && \
#     apt-get install -y --no-install-recommends \
#     curl \
#     && rm -rf /var/lib/apt/lists/*

# # Install Poetry
# RUN curl -sSL https://install.python-poetry.org | python3 -

# # Add Poetry to the PATH
# ENV PATH="/root/.local/bin:$PATH"

# # Copy the rest of the application code into the container
# COPY . /app

# # Install the dependencies using Poetry
# RUN poetry install

# # Make sure the prestart script is executable
# RUN chmod +x ./prestart.sh

# # Expose the port the app runs on
# EXPOSE 8000

# # Run the prestart script and start the server
# CMD ["sh", "-c", "poetry run bash ./prestart.sh && poetry run uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload"]



# Use Python 3.10 image as base
FROM python:3.10

# Set the working directory in the container
WORKDIR /app

# Install curl, bash, and dos2unix
RUN apt-get update -y && \
    apt-get install -y --no-install-recommends \
    curl \
    dos2unix \
    && rm -rf /var/lib/apt/lists/*

# Install Poetry
RUN curl -sSL https://install.python-poetry.org | python3 -

# Add Poetry to the PATH
ENV PATH="/root/.local/bin:$PATH"

# Copy the rest of the application code into the container
COPY . /app

# Convert Windows line endings in shell scripts to Unix format
RUN dos2unix ./prestart.sh && chmod +x ./prestart.sh

# Install the dependencies using Poetry
RUN poetry install

# Expose the port the app runs on
EXPOSE 8000

# Run the prestart script and start the server
CMD ["sh", "-c", "poetry run bash ./prestart.sh && poetry run uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload"]

