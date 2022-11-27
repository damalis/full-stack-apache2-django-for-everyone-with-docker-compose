FROM python:3.11

ENV TZ=${LOCAL_TIMEZONE}
	
RUN python -m pip install --upgrade pip

WORKDIR /usr/src/app

RUN apt-get update -y && \
	apt-get install -y \
		python3-dev \
		default-libmysqlclient-dev \
		build-essential \
		&& rm -rf /var/lib/apt/lists/*

COPY ./requirements.txt .

RUN python -m pip install -r requirements.txt

RUN useradd -U html
ENV APP_HOME=/home/html

WORKDIR $APP_HOME

RUN django-admin startproject webapp

EXPOSE 9000
CMD ["@"]
