FROM --platform=linux/amd64 ubuntu:20.04 as builder

RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y build-essential git

RUN git clone https://github.com/mirrorer/afl
WORKDIR /afl
RUN make && make install

COPY . /repo
WORKDIR /repo
RUN make -f /repo/test/fuzz/Makefile

FROM ubuntu:20.04 as package
COPY --from=builder /repo/.build/fuzz/mpack-fuzz /repo/.build/fuzz/mpack-fuzz
