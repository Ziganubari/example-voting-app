FROM python:3.11.9-slim-bookworm

# add apache bench (ab) tool
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    apache2-utils \
    && rm -rf /var/lib/apt/lists/*

RUN groupadd --system --gid 10001 app && \
    useradd --system --uid app --uid 10001 --no-create-home --shell /usr/sbin/nologin app


WORKDIR /seed

COPY . .

# create POST data files with ab friendly formats
RUN python make-data.py && chown -R app:app /seed
USER app 

CMD ["/seed/generate-votes.sh"]
