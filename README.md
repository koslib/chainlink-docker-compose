# chainlink-docker-compose
Simple docker-compose-based project to get quickly up and running a Chainlink node. This is intended mainly for development use, or at least should be enough to get you started with a working-as-is repository. However, it assumes basic Docker skills.

# How to use

1. Clone repository
```
git clone https://github.com/koslib/chainlink-docker-compose
```

1. Review `chainlink.env` and adapt accordingly. The committed environment file uses Rinkeby testnet. Also, the example uses Linkpool's public Ethereum service node.

2. Build and run with docker-compose

* Build with default values, which you can adapt if needed inside the `Dockerfile`
```
docker-compose up --build
```

* First build with your own build args and then run:

```
$ docker-compose build --build-arg API_USER_EMAIL=my@test.com

$ docker-compose up
```

4. Browse to `localhost:6688` and log in with your credentials.

Default credentials:
- username: `user@example.com`
- password: `PA@SSword1234!567`
- wallet password: `PA@SSword1234!567`

# Run with your own Ethereum local node

1. Add the following into `docker-compose.yaml`:

- Service:
```
ethereum:
    image: ethereum/client-go:v1.10.1
    ports:
      - 8546:8546
    command: --ropsten --syncmode light --ws --ipcdisable --ws.addr 0.0.0.0 --ws.origins="*" --datadir /geth
    volumes: 
      - geth:/geth
```

- Volume:
```
geth:
```

So the end result would be:
```
volumes: 
  geth:
  db-data:
  chainlink_data:
```

2. Change `ETH_URL` inside `chainlink.env` to:
```
ETH_URL=ws://ethereum:8546
```

3. Run again:

```
$ docker-compose up --build
```

# Disclaimer

This is a basic setup to quickly get you up and running with a Chainlink local node for development. Please acknolwedge that this setup does not take into account any node security nor high-availability (HA) settings, therefore cannot be used in production as is.

# Contributions

Feel free to open issues with questions or send in PRs in case you have an idea!

# Licence

MIT Licence