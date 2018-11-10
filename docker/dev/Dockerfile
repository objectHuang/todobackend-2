FROM objecthuang/todobackend-base:latest

#Install dev/build dependencies
RUN apt-get update && \
    apt-get install -qy python-dev libmysqlclient-dev

# Activate virtual environment and Install wheel support
RUN . /appenv/bin/activate && \
    pip install wheel --upgrade


#PIP enviroment variables (NOTE: must be set after installing wheel)
ENV WHEELHOURSE=/wheelhouse PIP_WHEEL_DIR=/wheelhouse PIP_FIND_LINKS=/wheelhouse XDG_CACHE_HOME=/cache

# OUTPUT: Build artificats (Wheels) are output here
VOLUME /wheelhouse

# OUTPUT: build cache
VOLUME /build

# OUTPUT: Test reports are output here
VOLUME /reports

COPY scripts/test.sh /usr/local/bin/test.sh
RUN chmod +x /usr/local/bin/test.sh

ENTRYPOINT [ "test.sh" ]
CMD ["python", "manage.py", "test", "--noinput"]

# Add application source
COPY src /application
WORKDIR /application