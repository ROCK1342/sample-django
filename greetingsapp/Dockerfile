# Use the official Ubuntu image as a base
FROM ubuntu:latest

# Set the working directory inside the container
WORKDIR /app

# Install dependencies for Python, pip, and virtual environment
RUN apt update && \
    apt install -y python3 python3-pip python3-venv

# Copy only the requirements.txt file first (this optimizes the build cache)
COPY requirements.txt /app/

# Create a virtual environment in the container
RUN python3 -m venv /venv

# Install the Python dependencies inside the virtual environment
RUN /venv/bin/pip install --upgrade pip && \
    /venv/bin/pip install -r /app/requirements.txt

# Now copy the rest of the application code (after dependencies)
COPY . /app

# Expose port 8000 for Django to run
EXPOSE 8000

# Set the entrypoint to use the virtual environment for running Django
ENTRYPOINT ["/venv/bin/python3", "/app/manage.py"]

# Default command to run Django's development server
CMD ["runserver", "0.0.0.0:8000"]
