# Set Python runtime as parent image.
FROM miniconda-image

# Set working directory.
WORKDIR /app

# Copy content of current directory into container's /app directory.
COPY . /app

# Create a new directory, download, install and initialise Miniconda
RUN conda create -y -n xeus-cling python=3.7
RUN conda install -n xeus-cling jupyter
RUN conda install -n xeus-cling xeus-cling -c conda-forge



# Expose one port to the world outside the container.
EXPOSE 8888

# Define an environment variable.
ENV OWN_IP 0.0.0.0

# Run a Jupyter notebook when the container launches.
# CMD ["jupyter", "notebook", "--ip=0.0.0.0", "--port=8888", "--allow-root", "--NotebookApp.token=''"]
