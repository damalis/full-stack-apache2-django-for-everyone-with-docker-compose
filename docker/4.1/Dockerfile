FROM python:3.11
LABEL maintainer="damalis"

ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
ENV TZ=${LOCAL_TIMEZONE}

RUN apt-get update -y && \
    apt-get install -y \
                python3-dev \
                default-libmysqlclient-dev \
                build-essential \
                --no-install-recommends \
                && rm -rf /var/lib/apt/lists/*

RUN adduser --disabled-password --gecos '' html

USER html

ENV PATH="$PATH:/home/html/.local/bin"

RUN pip install --upgrade pip

COPY --chown=html:html ./requirements.txt /tmp/requirements.txt

WORKDIR /app
EXPOSE 9000

RUN pip install --no-cache-dir -r /tmp/requirements.txt \
		&& rm -rf /tmp/*

COPY --chown=html:html . .
