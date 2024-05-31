FROM ubuntu:latest

RUN apt-get update && apt-get install -y \
    && apt-get install -y socat \
    && apt-get clean -y

RUN useradd -d /home/challenge -m -s /bin/bash challenge

COPY deps/limits.conf /etc/security/limits.d/90-challenge.conf

WORKDIR /home/challenge

COPY gopher_overflow .
COPY flag.txt .

RUN chmod -R 755 /home/challenge
RUN chmod 444 flag.txt
RUN chmod 111 gopher_overflow

RUN chown -R root:root /home/challenge

USER challenge

CMD ["socat", "TCP-LISTEN:9999,reuseaddr,fork", "EXEC:./gopher_overflow,stderr"]
EXPOSE 9999