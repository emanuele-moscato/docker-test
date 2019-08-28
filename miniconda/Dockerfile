# Set Python runtime as parent image.
FROM python:3.7.3

# Set working directory.
WORKDIR /app

# Copy content of current directory into container's /app directory.
COPY . /app

SHELL ["/bin/bash", "-c"]

# Create a new directory, download, install and initialise Miniconda
RUN mkdir /app/downloads
RUN wget -P /app/downloads/ https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
RUN bash /app/downloads/Miniconda3-latest-Linux-x86_64.sh -b
ENV PATH=/root/miniconda3/bin:$PATH
RUN conda init bash
RUN source /root/.bashrc
RUN conda create -y -n test-env python=3.7
RUN conda install -n test-env jupyter


# Expose one port to the world outside the container.
EXPOSE 8888

# Define an environment variable.
ENV OWN_IP 0.0.0.0

# Run a Jupyter notebook when the container launches.
# CMD ["jupyter", "notebook", "--ip=0.0.0.0", "--port=8888", "--allow-root", "--NotebookApp.token=''"]
