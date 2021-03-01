# Pocket Docker
*Easy deployment of multiple Pocket Network nodes via docker-compose*

## Files to change

### ./node-shared/chains.json

- Change the chains.json to reflect the chains you are serving and the location of the data node.

### ./docker-compose.yml

- Change PRIVATE_KEYs to your staked node's private keys
- If using a separate data storage device, change the location where Docker is storing the node data: 
```"./node-1/data:/home/app/.pocket/data"```

## File ownership

The data directory must be owned by the process running Pocket inside of Docker. On Ubuntu 18.04, this is user 1001 and user group 1005.

```CHOWN -R 1001:1005 ./node-1/data/```
```CHOWN -R 1001:1005 ./node-2/data/```

## To build

```./build.sh 1.13 RC-0.5.2.10 poktnetwork/pocket-core rc-0.5.2.10```

## To run

docker-compose up -d
