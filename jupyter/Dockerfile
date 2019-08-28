# Set Python runtime as parent image.
FROM python:3.7.3

# Set working directory.
WORKDIR /app

# Copy content of current directory into container's /app directory.
COPY . /app

# Install some Python packages from a requirements file.
RUN pip install --trusted-host pypi.python.org -r requirements.txt

# Expose one port to the world outside the container.
EXPOSE 8888

# Define an environment variable.
ENV OWN_IP 0.0.0.0

# Run a Jupyter notebook when the container launches.
CMD ["jupyter", "notebook", "--ip=0.0.0.0", "--port=8888", "--allow-root", "--NotebookApp.token=''"]
