FROM resin/rpi-raspbian

RUN apt-get update && apt-get install -y --no-install-recommends \
        build-essential \
        curl \
        libfreetype6-dev \
        libfreetype6-dev \
        libfribidi-dev \
        libharfbuzz-dev \
        libjpeg62-turbo-dev \
        liblcms2-dev \
        libpng12-dev \
        libtiff5-dev \
        libwebp-dev \
        libzmq3-dev \
        pkg-config \
        protobuf-compiler \
        python \
        python-dev \
        python-lxml \
        python-numpy \
        python-pip \
        python-scipy \
        python-tk \
        rsync \
        tcl8.6-dev \
        tk8.6-dev \
        unzip \
        zlib1g-dev

RUN pip --no-cache-dir install --upgrade \
        ipykernel \
        jupyter \
        wheel \
        Pillow \
        matplotlib && \
            python -m ipykernel.kernelspec

RUN wget https://github.com/samjabrahams/tensorflow-on-raspberry-pi/releases/download/v1.1.0/tensorflow-1.1.0-cp27-none-linux_armv7l.whl && \
    sudo pip install tensorflow-1.1.0-cp27-none-linux_armv7l.whl && \
    rm -rf tensorflow-1.1.0-cp27-none-linux_armv7l.whl

COPY jupyter_notebook_config.py /root/.jupyter/

# Copy sample notebooks.
COPY notebooks /notebooks

# Jupyter has issues with being run directly:
#   https://github.com/ipython/ipython/issues/7062
# We just add a little wrapper script.
COPY run_jupyter.sh /

# TensorBoard
EXPOSE 6006
# IPython
EXPOSE 8888

WORKDIR "/notebooks"

CMD ["/run_jupyter.sh", "--allow-root"]
