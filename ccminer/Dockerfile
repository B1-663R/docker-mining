FROM alpine/git as repo
WORKDIR /app/repo/
RUN git clone https://github.com/tpruvot/ccminer.git

FROM nvidia/cuda:9.1-base as build
WORKDIR /app/src/
COPY --from=repo /app/repo/ccminer .
RUN apt-get update
RUN apt-get install -qq --no-install-recommends -y cuda-compiler-9-1 cuda-cudart-dev-9-1
RUN apt-get install -qq --no-install-recommends -y libcurl4-openssl-dev libssl-dev libjansson-dev automake autotools-dev build-essential
RUN ln -sf /usr/local/cuda/targets/x86_64-linux/lib/stubs/libcuda.so /usr/lib/
RUN ./autogen.sh
RUN ./configure --with-cuda=/usr/local/cuda && make -j$(($(nproc)+1))

FROM nvidia/cuda:9.1-base as bin
WORKDIR /app/
COPY --from=build /app/src/ccminer /app/
RUN apt-get update
RUN apt-get install -qq --no-install-recommends -y ca-certificates libssl-dev libcurl4-openssl-dev libjansson-dev libgomp1
ENTRYPOINT ["/app/ccminer"]