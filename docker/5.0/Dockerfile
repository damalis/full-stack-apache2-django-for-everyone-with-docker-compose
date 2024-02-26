FROM python:3.12.2
LABEL maintainer="damalis"

ENV DEBIAN_FRONTEND noninteractive
ENV DEBCONF_NOWARNINGS="yes"
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
ENV TZ=${TZ}

RUN set -ex && apt-get update && \
    apt-get install -y apt-utils \
		--no-install-recommends \
		python3-dev \
		default-libmysqlclient-dev \
		build-essential \
		&& rm -rf /var/lib/apt/lists/*

RUN adduser --disabled-password --gecos '' html

USER html

ENV PATH /home/html/.local/bin:$PATH

RUN pip install --upgrade pip

COPY --chown=html:html ./requirements.txt /tmp/requirements.txt

WORKDIR /app
EXPOSE 9000

RUN pip install --no-cache-dir -r /tmp/requirements.txt \
                && rm -rf /tmp/*

COPY --chown=html:html . .
