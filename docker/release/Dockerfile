FROM objecthuang/todobackend-base:latest

COPY target /wheelhouse

RUN . /appenv/bin/activate && \
    pip install --no-index -f /wheelhouse todobackend && \
    rm -rf /wheelhouse