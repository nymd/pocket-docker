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

The data directory must be owned by the process running Pocket inside of Docker. On Ubuntu 20.04, this is user 1005 and user group 1001.

```CHOWN -R 1005:1001 ./node-1/data/```
```CHOWN -R 1005:1001 ./node-2/data/```

## To run

docker-compose up -d
