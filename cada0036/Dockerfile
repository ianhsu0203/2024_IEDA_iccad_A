FROM --platform=linux/amd64 ubuntu:20.04
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y \
    nano \
    python3 \
    python3-pip \
    python3-venv \
    build-essential \
    git \
    libreadline-dev \
    && rm -rf /var/lib/apt/lists/*

COPY . /app
WORKDIR /app
RUN python3 -m venv venv
RUN . ./venv/bin/activate && pip install --no-cache-dir -r requirements.txt
RUN rm -rf /app/abc
RUN git clone https://github.com/berkeley-abc/abc.git /app/abc && \
    cd /app/abc && \
    make
RUN chmod +x /app/cost_estimators/*
RUN . ./venv/bin/activate && pip install --no-cache-dir opentuner \
    numpy \
    scipy \
    matplotlib \
    sqlalchemy

ENV PYTHONUNBUFFERED=1
CMD ["/bin/bash"]
