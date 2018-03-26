FROM alpine/git as repo
WORKDIR /app/repo/
RUN git clone https://github.com/ethereum-mining/ethminer.git
RUN cd ethminer && git submodule update --init --recursive

FROM nvidia/cuda:9.1-base as build
ENV ETHMINER_CMAKE_FLAGS -DETHASHCUDA=ON -DETHASHCL=OFF
RUN apt-get update \
    && set -x \
    && apt-get install -qq --no-install-recommends -y ca-certificates cmake cuda-core-9-1 cuda-cudart-dev-9-1 libssl-dev
WORKDIR /src/
COPY --from=repo /app/repo/ethminer ethminer/
RUN cd ethminer && cmake . -DETHASHCUDA=ON -DETHASHCL=OFF
RUN cd ethminer && cmake --build .

FROM nvidia/cuda:9.1-base as bin
RUN apt-get update \
    && apt-get install -qq --no-install-recommends -y cuda-core-9-1
COPY --from=build /src/ethminer/ethminer /app/
WORKDIR /app/
ENTRYPOINT ["/app/ethminer"]