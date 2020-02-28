FROM docker:dind

RUN apk --no-cache add \
      git \
      findutils \
      attr && \
    rm -rf /var/cache/apk/*

RUN apk add python3

RUN pip3 install --upgrade pip && pip3 install tern

CMD ["sh"]  