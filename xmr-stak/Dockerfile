FROM alpine/git as repo
WORKDIR /app/repo/
RUN git clone https://github.com/fireice-uk/xmr-stak.git

FROM nvidia/cuda:9.1-base as build
ENV XMRSTAK_CMAKE_FLAGS -DXMR-STAK_COMPILE=generic -DCUDA_ENABLE=ON -DOpenCL_ENABLE=OFF
RUN apt-get update \
    && set -x \
    && apt-get install -qq --no-install-recommends -y ca-certificates cmake cuda-core-9-1 git cuda-cudart-dev-9-1 libhwloc-dev libmicrohttpd-dev libssl-dev curl
WORKDIR /mnt/
COPY --from=repo /app/repo/xmr-stak xmr-stak/
RUN cd xmr-stak && cmake ${XMRSTAK_CMAKE_FLAGS} . && make

FROM nvidia/cuda:9.1-base as bin
RUN apt-get update \
    && apt-get install -qq --no-install-recommends -y cuda-core-9-1 libmicrohttpd-dev libssl-dev libhwloc-dev
COPY --from=build /mnt/xmr-stak/bin/* /usr/local/bin/
WORKDIR /mnt
ENTRYPOINT ["/usr/local/bin/xmr-stak"]