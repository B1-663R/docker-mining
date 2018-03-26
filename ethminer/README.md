### Build image

`$ sudo docker build -t docker-miner/ethminer .`


### How to start

Latest Release

~~~~
$ cd ethminer
$ sudo nvidia-docker run -it docker-miner/ethminer -U --farm-recheck 200 -S eu1.ethermine.org:4444 -FS us1.ethermine.org:4444 -O 0x8866bDaDD8BE0F6C4A580F079981F7a084e25B73.lab-eth
~~~~

Adapt the command with your setings
