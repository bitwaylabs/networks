*** Important ***  

This document is incomplete and will be completed before 10:00 AM UTC on August 19, 2025.

If you are upgrading from sidechain-1, please make sure that your validator pubkey does not change and just use the old priv_validator_key.json file to run the Bitway node.

# Mainnet: bitway-1

## Get Started

### Prerequisite‌

1. Install Golang

   ```sh
   go version 1.23.0+ is required.
   ```

   Refer to the [official install documentation](https://golang.google.cn/doc/install).

### Cloning BITWAY Repository and Setup

1. Clone the BITWAY repository:

   ```sh
   git clone https://github.com/bitwaylabs/bitway.git
   ```

2. Move to the BITWAY directory:

   ```sh
   cd bitway
   ```

3. Checkout to the desired version:

   ```sh
   git checkout v2.0.0
   ```

4. Install BITWAY:

   ```sh
   make install
   ```

5. Verify installation:

   ```sh
   bitwayd version --long
   ```

   ```sh
   commit: <Undetermined>
   cosmos_sdk_version: v0.50.12
   go: go version go1.23.0 linux/amd64
   name: bitway
   server_name: bitwayd
   version: 2.0.0
   ```

   > Note: The commit for `v2.0.0` is `<Undetermined>`

### Launch

1. Download the genesis file:

   ```sh
   wget https://github.com/bitwaylabs/networks/raw/main/mainnet/bitway-1/genesis.json -O ~/.bitway/config/genesis.json
   ```

   > This genesis file will be completed before the official launch of the bitway-1 network.

2. Verify the SHA256 hash of the downloaded genesis file:

   ```sh
   shasum -a 256 ~/.bitway/config/genesis.json
   ```

   Expected output:

   ```sh
   <To be added> genesis.json   
   ```

3. Set up the persistent peers:

   Set `persistent_peers` in `<home>/config/config.toml` to the following peer:

   ```sh
   <To be added>
   ```

   > Tip: More peers can be found through [Community Peers](https://itrocket.net/services/mainnet/bitway/#peers).

4. Start node:

   ```sh
   bitwayd start
   ```

   > Note: For validators, `minimum-gas-prices` is required and `0.0006ubtw,0.000001sat` is recommended. You can set it in `<home>/config/app.toml` or start with the flag:

   ```sh
   bitwayd start --minimum-gas-prices=0.0006ubtw,0.000001sat
   ```

### Create a new Validator

1. Create the validator address

   ```sh
   bitwayd keys add <key name> --key-type=<key type>
   ```

   > Note: The key type can be `Segwit` or `Taproot`.

2. Create Validator

   > Note: Please fund the above generated address first.

   Place the validator info to a JSON file:

   ```sh
   {
         "pubkey": {"@type":"/cosmos.crypto.ed25519.PubKey","key":"<PUBLIC KEY>"},
         "amount": "<AMOUNT>",
         "moniker": "<MONIKER>",
         "identity": "optional identity signature (ex. UPort or Keybase)",
         "website": "validator's (optional) website",
         "security": "validator's (optional) security contact email",
         "details": "validator's (optional) details",
         "commission-rate": "0.1",
         "commission-max-rate": "0.2",
         "commission-max-change-rate": "0.01",
         "min-self-delegation": "1"
   }
   ```

   > Note: The public key can be obtained via the following command:

   ```sh
   bitwayd comet show-validator
   ```

   Create validator with the specified path:

   ```sh
   bitwayd tx staking create-validator <path/to/validator.json> --from <KEY_NAME> --chain-id bitway-1 --fees 1000ubtw
   ```

### Inherited validator from sidechain-1

1. Reuse the priv_validator_key.json

   ```sh
   cp ~/.side/config/priv_validator_key.json ~/.bitway/config/priv_validator_key.json
   ```

2. Start node:

   ```sh
   bitwayd start
   ```
