FROM python:3.8-slim

RUN mkdir /code
WORKDIR /code

ENV DEBCONF_NOWARNINGS yes
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

COPY ./entrypoint.sh /code/app/entrypoint.prod.sh
COPY requirements.txt /code/

RUN apt-get update && apt-get install -y libpq-dev build-essential libssl-dev libffi-dev libblas3 libc6 liblapack3 gcc
RUN apt-get install -y netcat
RUN pip install --upgrade pip \
    && pip install -r requirements.txt
RUN apt-get autoremove -y gcc

COPY . /code/

ENTRYPOINT ["/bin/bash", "/code/entrypoint.sh"]