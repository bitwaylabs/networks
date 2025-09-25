# Bitway Upgrade Announcement V2.0.1 (Mainnet)

## We plan to upgrade the chain at the following time

Thursday, September 25, 2025, 13:00 UTC.
Bitway height: 3424000.

## The upgrade contents are as follows

  - Remove the wasm module
  - Integrate Hyperlane module
  - Unjail slashed validators (Ping Pub & HashKey Cloud) due to the app hash issue during the hard-fork upgrade

## Please follow the steps below to perform the upgrade

### 1. Checkout your bitway to V2.0.1 branch.

  ```sh
  cd ~/bitway
  git fetch --tags
  git checkout v2.0.1
  make install
  ```

### 2. Check your bitway version.

  ```sh
  ~/go/bin/bitwayd version --long
  ```

  Expected output:
  ```sh
  commit: 07f2bb1d0c6a8a2de3e89730cf60a8ba4b381fa8
  cosmos_sdk_version: v0.50.14
  go: go version go1.23.0 linux/amd64
  name: bitway
  server_name: bitwayd
  version: 2.0.1
  ```

### 3. Start your bitway node.

  ```sh
  ~/go/bin/bitwayd start
  ```
