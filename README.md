# Tnetc Launch Coin Snipe

Automated token sniper system for Solana using Believe Protocol.

## Installation with Docker

### Build Image

```bash
docker build -t tnetc-launch-coin-snipe .
```

### Run Container

There are two main ways to run the container:

#### 1. Using .env file

The simplest way is to use an existing .env file:

```bash
docker run -d --name tnetc-launch-coin-sniper --env-file .env tnetc-launch-coin-snipe
```

#### 2. Passing environment variables directly

```bash
docker run -d --name tnetc-sniper \
  -e RPC_URL=https://api.mainnet-beta.solana.com \
  -e SNIPE_WALLET_PK=your_private_key \
  -e CREATOR_WALLET=your_creator_wallet \
  -e TOKEN_TICKER=your_token_ticker \
  -e AMOUNT_IN=0.01 \
  -e SLIPPAGE=1 \
  -e REDIS_HOST=localhost \
  -e REDIS_PORT=6379 \
  -e REDIS_DB=2 \
  tnetc-launch-coin-snipe
```

## Required Environment Variables

| Variable | Description | Example |
|----------|-------------|---------|
| RPC_URL | Solana RPC endpoint URL | https://api.mainnet-beta.solana.com |
| SNIPE_WALLET_PK | Private key of Solana wallet for transactions | your_base58_private_key |
| CREATOR_WALLET | Creator wallet address for token filtering | GJ9mv8t1WRC1RUmKto5h5EnaRPSt2t6VpDyvp3VJ3gwD |
| TOKEN_TICKER | Token ticker/symbol for filtering (optional) | meomeo |
| AMOUNT_IN | Amount of SOL to snipe new tokens | 0.01 |
| SLIPPAGE | Allowed slippage percentage for transactions | 1 |
| REDIS_HOST | Redis server hostname | localhost |
| REDIS_PORT | Redis server port | 6379 |
| REDIS_DB | Redis database index | 2 |

## Container Logs

View container logs:

```bash
docker logs tnetc-sniper
```

## Container Management

Stop the container:

```bash
docker stop tnetc-sniper
```

Restart the container:

```bash
docker start tnetc-sniper
```

## Security Notes

* Do not store private keys in .env files that are pushed to git repositories
* Consider using Docker secrets in production environments
* Use reliable RPC Nodes to avoid "Blockhash not found" errors

## Fee per transaction

* Each snipe transaction, if you succeed in sniping your token, will automatically transfer 10% of your token's allocation to the treasury wallet. Read carefully before using this tool!
