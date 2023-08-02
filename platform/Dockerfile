FROM python:3.11-slim-buster as prod

RUN apt-get update && apt-get install -y \
  default-libmysqlclient-dev \
  pkg-config \
  gcc \
  ca-certificates \
  pkg-config \
  openjdk-11-jdk \
  && rm -rf /var/lib/apt/lists/*

RUN pip install -i https://mirrors.aliyun.com/pypi/simple/ poetry==1.4.2

# Configuring poetry
# RUN poetry config --global repositories.ali https://mirrors.aliyun.com/pypi/simple/

RUN poetry config virtualenvs.create false

# Copying requirements of a project
COPY pyproject.toml /app/src/
COPY openai-0.27.8 /app/openai-0.27.8
WORKDIR /app/src

# Installing requirements
RUN poetry install --only main
# Removing gcc
RUN apt-get purge -y \
  gcc \
  pkg-config \
  && rm -rf /var/lib/apt/lists/*

# Copying actual application
COPY . /app/src/
RUN poetry install --only main

CMD ["/usr/local/bin/python", "-m", "reworkd_platform"]

FROM prod as dev

RUN poetry install
