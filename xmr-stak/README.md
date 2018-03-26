### Build image

`# docker build -t docker-mining/xmr-stak:latest .`

### Test POW 

`# docker build -f Dockerfile-pow -t docker-mining/xmr-stak:pow .`


### How to start

Latest Release

~~~~
$ cd xmr-stak
# nvidia-docker run --rm -it -v "$PWD":/mnt docker-mining/xmr-stak:latest

Follow Instructions
~~~~

Dev branch or testing branch

~~~~
$ cd xmr-stak/pow
# nvidia-docker run --rm -it -v "$PWD":/mnt docker-mining/xmr-stak:pow

Follow instructions
~~~~