# Believe Launch Coin Snipe

[![Docker Pulls](https://img.shields.io/docker/pulls/andrewpixel/believe-launch-coin-snipe)](https://hub.docker.com/r/andrewpixel/believe-launch-coin-snipe)
[![Docker Image Size](https://img.shields.io/docker/image-size/andrewpixel/believe-launch-coin-snipe/latest)](https://hub.docker.com/r/andrewpixel/believe-launch-coin-snipe)

Automated token sniper system for Solana using the Believe Protocol. This tool helps you automatically detect and purchase new token launches on the Solana blockchain.

## Features

- Automated detection of new token launches
- Configurable token filtering by creator wallet or token ticker
- Customizable purchase amount and slippage settings
- Redis-based job queue for reliable transaction processing
- Real-time transaction monitoring and logging

## Quick Start

### Pull the Docker Image

```bash
docker pull andrewpixel/believe-launch-coin-snipe
```

### Run with Environment Variables

```bash
docker run -d --name believe-sniper \
  -e RPC_URL=https://api.mainnet-beta.solana.com \
  -e SNIPE_WALLET_PK=your_private_key \
  -e CREATOR_WALLET=your_creator_wallet \
  -e TOKEN_TICKER=your_token_ticker \
  -e AMOUNT_IN=0.01 \
  -e SLIPPAGE=1 \
  -e REDIS_HOST=localhost \
  -e REDIS_PORT=6379 \
  -e REDIS_DB=2 \
  andrewpixel/believe-launch-coin-snipe
```

### Run with .env File

Create a `.env` file with the required variables:

```
RPC_URL=https://api.mainnet-beta.solana.com
SNIPE_WALLET_PK=your_private_key
CREATOR_WALLET=your_creator_wallet
TOKEN_TICKER=your_token_ticker
AMOUNT_IN=0.01
SLIPPAGE=1
REDIS_HOST=localhost
REDIS_PORT=6379
REDIS_DB=2
```

Then run:

```bash
docker run -d --name believe-sniper --env-file .env andrewpixel/believe-launch-coin-snipe
```

## Configuration Options

| Variable | Description | Required | Default | Example |
|----------|-------------|----------|---------|---------|
| RPC_URL | Solana RPC endpoint URL | Yes | - | https://api.mainnet-beta.solana.com |
| SNIPE_WALLET_PK | Private key of Solana wallet for transactions | Yes | - | your_base58_private_key |
| CREATOR_WALLET | Creator wallet address for token filtering | Yes | - | GJ9mv8t1WRC1RUmKto5h5EnaRPSt2t6VpDyvp3VJ3gwD |
| TOKEN_TICKER | Token ticker/symbol for filtering | No | - | meomeo |
| AMOUNT_IN | Amount of SOL to snipe new tokens | Yes | - | 0.01 |
| SLIPPAGE | Allowed slippage percentage for transactions | Yes | 1 | 1 |
| REDIS_HOST | Redis server hostname | Yes | localhost | localhost |
| REDIS_PORT | Redis server port | Yes | 6379 | 6379 |
| REDIS_DB | Redis database index | Yes | 0 | 2 |

## Docker Management Commands

### View Logs

```bash
docker logs believe-sniper
```

### Stop Container

```bash
docker stop believe-sniper
```

### Restart Container

```bash
docker start believe-sniper
```

### Remove Container

```bash
docker rm believe-sniper
```

## Redis Requirements

The tool requires a Redis instance for operation. You can run Redis in a separate container:

```bash
docker run -d --name redis -p 6379:6379 redis
```

Or use an existing Redis instance by configuring the connection details in the environment variables.

## Advanced Configuration

### Using a Custom RPC Node

For improved reliability and performance, consider using a dedicated RPC node:

```bash
docker run -d --name believe-sniper \
  -e RPC_URL=https://your-custom-rpc-node.com \
  ... (other variables) \
  andrewpixel/believe-launch-coin-snipe
```

### Monitoring Multiple Creator Wallets

To monitor multiple creator wallets, run separate containers with different configurations.

## Fee Structure

**Important:** Each successful snipe transaction automatically transfers 10% of your token allocation to the developer's treasury wallet as a fee for using the tool.

## Security Considerations

- **Private Keys**: Never store private keys in environment files that are pushed to public repositories
- **Docker Secrets**: For production deployments, consider using Docker secrets
- **RPC Reliability**: Use reliable RPC nodes to avoid "Blockhash not found" errors
- **Fund Management**: Only allocate funds you can afford to risk

## Troubleshooting

Common issues:

1. **Connection Errors**: Check your RPC_URL and ensure it's reliable
2. **Transaction Failures**: Verify you have sufficient SOL balance for transactions
3. **Redis Connection**: Ensure Redis is accessible from the container
4. **Missing Tokens**: Verify creator wallet address is correct

## Disclaimer

This tool is for educational and experimental purposes only. Trading crypto tokens involves significant risk. Use at your own risk.

## License

This project is proprietary software. Usage of this tool implies acceptance of the fee structure mentioned above.

## Support

For issues and support, please open an issue in the GitHub repository or contact the developer directly.
