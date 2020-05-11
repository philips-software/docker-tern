FROM docker:dind

RUN apk --no-cache add \
      git \
      findutils \
      util-linux \
      tar \
      cifs-utils \
      nfs-utils \
      attr && \
      rm -rf /var/cache/apk/*

RUN apk add python3

RUN pip3 install --upgrade pip && pip3 install -Iv tern==2.0.0

ADD REPO .
ADD TAGS .

RUN mkdir hostmount

ENTRYPOINT ["tern", "-b", "/hostmount"]
CMD ["-h"]
