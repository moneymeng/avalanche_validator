# Running an Avalanche Validator

This guide explains how to set up and run an Avalanche validator node.

## Prerequisites
Before starting, ensure you have the following:
- A computer with at least:
  - 8-core CPU
  - 16GB RAM
  - 1TB SSD (NVMe recommended)
  - Stable internet connection with at least 10 Mbps upload/download
- Ubuntu 20.04 or later (recommended)
- Static public IP address
- At least 2,000 AVAX to stake
- Open ports: `9651` (RPC), `9650` (P2P)

## Step 1: Install AvalancheGo
1. Update and install dependencies:
   ```sh
   sudo apt update && sudo apt upgrade -y
   sudo apt install curl jq git -y
   ```
2. Download and install AvalancheGo:
   ```sh
   curl -Lo avalanchego.tar.gz https://github.com/ava-labs/avalanchego/releases/latest/download/avalanchego-linux-amd64.tar.gz
   tar -xvf avalanchego.tar.gz
   sudo mv avalanchego /usr/local/bin/
   ```
3. Verify installation:
   ```sh
   avalanchego --version
   ```

## Step 2: Run the Validator Node
1. Create a data directory:
   ```sh
   mkdir ~/.avalanchego
   ```
2. Start the node:
   ```sh
   avalanchego --public-ip=<YOUR_STATIC_IP> --http-host=0.0.0.0
   ```
3. Ensure the node is running:
   ```sh
   curl -X POST --data '{"jsonrpc":"2.0","id":1,"method":"info.getNodeID"}' -H 'content-type: application/json;' 127.0.0.1:9650/ext/info
   ```

## Step 3: Add Your Node as a Validator
1. Obtain your `NodeID` from the previous step.
2. Go to [Avalanche Wallet](https://wallet.avax.network/), log in, and navigate to the “Earn” section.
3. Click **Add Validator**, enter your `NodeID`, stake at least 2,000 AVAX, and set delegation fees.
4. Confirm and wait for activation.

## Step 4: Monitor Your Node
- Check logs:
  ```sh
  tail -f ~/.avalanchego/logs/main.log
  ```
- Use Avalanche Stats API:
  ```sh
  curl -X POST --data '{"jsonrpc":"2.0","id":1,"method":"health.getLiveness"}' -H 'content-type: application/json;' 127.0.0.1:9650/ext/health
  ```

## Troubleshooting
- Ensure ports `9651` and `9650` are open.
- Restart the node if needed:
  ```sh
  pkill -f avalanchego && avalanchego --public-ip=<YOUR_STATIC_IP> --http-host=0.0.0.0
  ```
- Check official Avalanche [Discord](https://discord.gg/avalanche) or [Docs](https://docs.avax.network/) for help.

## Conclusion
Your Avalanche validator node is now running! Ensure uptime to earn staking rewards and monitor your node regularly.

