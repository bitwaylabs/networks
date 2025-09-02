
# Bitway

1. app.toml

    ```sh
    vi .bitway/config/app.toml
    ```

    ```sh
    ...
    minimum-gas-prices = "0.0006ubtw,0.000001sat"
    # Do not set too high gas prices to avoid transaction submission failures.
    ...

    [oracle]
    # If this node will act as a validator, set to true. For non-validator (full) nodes, set to false.
    enable = true
    bitcoin_rpc = "192.248.180.245:8332"
    bitcoin_rpc_user = "bitway"
    bitcoin_rpc_password = "12345678"
    http_post_mode = true
    disable_tls = true
    # Please replace it with your own bitcoin information
    ...

    # Keep other parameters as default.
    ```

2. config.toml

    ```sh
    vi .bitway/config/config.toml
    ```

    ```sh
    ...
    persistent_peers = "<To be added>"
    # You can get more peer nodes from the community.
    ...

    # Keep other parameters as default.
    ```

# TSSigner 

1. config.toml

    ```sh
    vi .shuttler/config.toml
    ```

    ```sh
    port = 5158
    enable_rpc = true
    rpc_address = "127.0.0.1:6780"
    bootstrap_nodes = [<To be added>]
    log_level = "debug"
    mnemonic = "<MNEMONIC>"
    priv_validator_key_path = "priv_validator_key.json"
    relay_runes = false
    last_scanned_height_side = 0
    last_scanned_height_bitcoin = 0
    loop_interval = 60
    batch_relayer_count = 10
    max_attempts = 5

    [bitcoin]
    network = "bitcoin"
    rpc = "http://192.248.180.245:8332"
    user = "bitway"
    password = "12345678"
    # Please replace it with your own bitcoin testnet information

    [bitway]
    grpc = "http://localhost:9090"
    rpc = "http://localhost:26657"
    gas = 1000000
    # Please replace it with your own side chain information

    [bitway.fee]
    amount = 1000
    denom = "ubtw"

    [ordinals]
    endpoint = ""

    [fee_provider]
    submit_fee_rate = false
    fetch_fee_rate_url = "https://mempool.space/api/v1/fees/recommended"
    ```

# Bitcoin

1. bitcoin.conf

    ```sh
    vi .bitcoin/bitcoin.conf
    ```

    ```sh
    testnet=0
    txindex=1

    [main]
    rpcbind=0.0.0.0:8332
    rpcallowip=0.0.0.0/0
    rpcuser=bitway
    rpcpassword=12345678
    ```
