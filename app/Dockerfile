# Use a minimal Python image
FROM python:3.10-slim

# Set the working directory
WORKDIR /app

# Copy application files
COPY . .

# Install dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Expose port (optional if your app uses 3000 or 5000)
EXPOSE 3000

# Run the app
CMD ["python", "app.py"]
