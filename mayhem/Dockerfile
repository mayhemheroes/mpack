FROM moflow/afl-tools as builder

RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y build-essential git

COPY . /repo
WORKDIR /repo
RUN make -f /repo/test/fuzz/Makefile

FROM moflow/afl-tools as package
COPY --from=builder /repo/.build/fuzz/mpack-fuzz /repo/.build/fuzz/mpack-fuzz
