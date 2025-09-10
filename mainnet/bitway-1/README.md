*** Important ***  

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
   commit: ebf5e00c2fcf6f8d2fc1f831979f10cda2113a7a
   cosmos_sdk_version: v0.50.14
   go: go version go1.23.0 linux/amd64
   name: bitway
   server_name: bitwayd
   version: 2.0.0
   ```

   > Note: The commit for `v2.0.0` is `ebf5e00c2fcf6f8d2fc1f831979f10cda2113a7a`

6. Copy to /usr/local/bin

   ```sh
   sudo cp ~/go/bin/bitwayd /usr/local/bin
   ```

   > Copy it to the /usr/local/bin directory to ensure that it can be used anywhere.

### Launch

1. Initialize the local node

   ```sh
   bitwayd init <Moniker> --home ~/.bitway
   ```

2. Reuse the old validator key

   ```sh
   cp ~/.side/config/priv_validator_key.json ~/.bitway/config/
   ```

   > If you are upgrading from sidechain-1, please reuse your old validator key.  
   > If not, please skip this step.

3. Download the genesis file:

   ```sh
   wget https://github.com/bitwaylabs/networks/raw/main/mainnet/bitway-1/genesis.tar.gz -O ~/.bitway/config/genesis.tar.gz
   ```

   > This genesis file will be completed before the official launch of the bitway-1 network.

4. Unzip the genesis file

   ```sh
   cd ~/.bitway/config
   tar xvfz genesis.tar.gz
   ```

5. Verify the SHA256 hash of the genesis file:

   ```sh
   shasum -a 256 ~/.bitway/config/genesis.json
   ```

   Expected output:

   ```sh
   2fc783fd26301f6c127514ab4e91e25105a98d6725f9122accaf42962b705359 genesis.json   
   ```

6. Set up the persistent peers in config.toml:

   Set `persistent_peers` in `<home>/config/config.toml` to the following peer:

   ```sh
   ab68cefc837ed11989dea304f2364e0f84d5124c@209.250.232.135:26656
   ac5e9176ea17ec6a0e5e60a91913c5638b1851e2@202.182.119.24:26656
   ```

   > Tip: More peers can be found through [Community Peers](https://itrocket.net/services/mainnet/bitway/#peers).

7. Set up bitcoin params for oracle in app.toml:  

   ```sh
    vi .bitway/config/app.toml
   ```

   At the end of the file:

   ```sh
   [oracle]
   # If this node will act as a validator, set to true. For non-validator (full) nodes, set to false.
   enable = true
   bitcoin_rpc = "192.248.180.245:8332"
   bitcoin_rpc_user = "bitway"
   bitcoin_rpc_password = "12345678"
   http_post_mode = true
   disable_tls = true
   # Please replace it with your own bitcoin information
   ```

8. Start node:

   ```sh
   bitwayd start
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

# Hardware Specifications

## Running the Bitway full node

1. Minimum Requirements

   - CPU: 8 cores

   - RAM: 16 GB

   - Storage: 200 GB

   - Network: 1 Gbps

   - SWP: 8GB

2. Recommended Specifications

   - CPU: 8 cores

   - RAM: 32 GB

   - Storage: 500 GB

   - Network: 1 Gbps

   - SWP: 8GB