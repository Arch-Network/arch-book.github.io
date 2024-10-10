# Starting the stack

Within [arch-cli], there exist 3 configuration files needed to provision the various services:
1. [arch-docker-compose.yml]
2. [bitcoin-docker-compose.yml]
3. [btc-rpc-explorer.dockerfile]

These files comprise the pre-configured, multi-container definition of the components required for standing up a local development environment.

### Configure

First, ensure that your Docker client is up-to-date and that the `DOCKER_DEFAULT_PLATFORM` environment variable is properly set (within your `~/.bashrc` or shell of choice) to your machine's architecture.

```bash
# Eg, for Apple-Silicon users:
export DOCKER_DEFAULT_PLATFORM=linux/amd64
```

#### Declare your `config.toml`

Before using `arch-cli`, you need to set up a `config.toml` file. By default, the CLI will look for this file in the following locations:
- Linux: ~/.config/arch-cli/config.toml
- macOS: ~/Library/Application Support/arch-cli/config.toml
- Windows: C:\Users\<User>\AppData\Roaming\arch-cli\config.toml

If the configuration file is not found, a default configuration file will be created automatically using the `config.default.toml` template which can then be renamed to `config.toml` if you don't wish to create your own.

You can also specify a custom configuration file location by setting the `ARCH_CLI_CONFIG` environment variable:

```bash
export ARCH_CLI_CONFIG=/path/to/your/config.toml
```

Here's an example configuration:

```toml
[network]
type = "development"  # Options: development, testnet, mainnet

[bitcoin]
docker_compose_file = "./bitcoin-docker-compose.yml"
network = "regtest"
rpc_endpoint = "http://localhost:18443"
rpc_port = "18443"
rpc_user = "bitcoin"
rpc_password = "password"
rpc_wallet = "devwallet"

[arch]
docker_compose_file = "./arch-docker-compose.yml"
leader_rpc_endpoint = "http://localhost:8080"
network_mode = "development"
rust_log = "info"
rust_backtrace = "1"
bootnode_ip = "127.0.0.1"
leader_p2p_port = "9000"
leader_rpc_port = "8080"
validator1_p2p_port = "9001"
validator1_rpc_port = "8081"
validator2_p2p_port = "9002"
validator2_rpc_port = "8082"
bitcoin_rpc_endpoint = "http://localhost:18443"
bitcoin_rpc_wallet = "devwallet"
replica_count = "3"

[program]
key_path = "src/app/keys/program.json"
```

By following these steps, you ensure that your CLI can be run from any location and still correctly locate and load its configuration files on Windows, macOS, and Linux.

### Initialize

The `init` subcommand sets up a new Arch Network project with the necessary folder structure, boilerplate code, and Docker configurations.

We'll invoke this and setup a new project.

```bash
arch-cli init
```

If everything initializes smoothly, you'll be presented with output similar to the following:
```bash
Welcome to the Arch Network CLI
  → Loading configuration from /Users/jr/Library/Application Support/arch-cli/config.toml
Initializing new Arch Network app...
Checking required dependencies...
  → Checking docker... ✓
    Detected version: Docker version 27.2.0, build 3ab4256958
  → Checking docker-compose... ✓
    Detected version: Docker Compose version 2.29.2
  → Checking node... ✓
    Detected version: v22.8.0
  → Checking solana... ✓
    Detected version: solana-cli 1.18.22 (src:b286211c; feat:4215500110, client:SolanaLabs)
  → Checking cargo... ✓
    Detected version: cargo 1.80.1 (376290515 2024-07-16)
All required dependencies are installed.
  ✓ Created arch-data directory at "/Users/jr/Library/Application Support/arch-cli/arch-data"
  ✓ Copied default configuration to "/Users/jr/Library/Application Support/arch-cli/config.toml"
Building Arch Network program...
Creating project structure...
Creating boilerplate files...
  ℹ Existing program directory found, preserving it
  ℹ Existing frontend directory found, preserving it
  ✓ New Arch Network app initialized successfully!
```

Your project should now have the following structure:
```bash
my-arch-project/
├── src/
│   └── app/
│       ├── program/
│       │   └── src/
│       │       └── lib.rs
│       ├── backend/
│       │   ├── index.ts
│       │   └── package.json
│       ├── frontend/
│       │   ├── index.html
│       │   ├── index.js
│       │   ├── package.json
│       │   └── .env.example
│       └── keys/
├── Cargo.toml
├── config.toml
├── bitcoin-docker-compose.yml
└── arch-docker-compose.yml
```

### Start the services

Now that the arch-cli is properly configured and we've initialized a new project, our next step will be to start the development cluster which will provision the Arch network nodes, an ordinals indexing service and a block explorer.

```bash
arch-cli server start
```

If everything pulls and builds correctly, you should see something resembling the following in your Docker client logs: 
```bash
Welcome to the Arch Network CLI
  → Loading configuration from /Users/jr/Library/Application Support/arch-cli/config.toml
Starting the development server...
  ✓ Bitcoin started.
[+] Running 10/10
 ✔ leader Pulled 6.7s
 ✔ validator-2 Pulled 6.7s
 ✔ validator-1 Pulled 6.7s
 ✔ init Pulled 6.7s
 ✔ bootnode Pulled 6.6s
[+] Running 7/7
 ✔ Network arch-cli_arch-network Created 0.0s
 ✔ Network arch-cli_default Created 0.0s
 ✔ Container arch-cli-init-1  Started 0.5s
 ✔ Container arch-cli-bootnode-1  Started 0.3s
 ✔ Container arch-cli-leader-1  Started 0.4s
 ✔ Container arch-cli-validator-1-1  Started 0.5s
 ✔ Container arch-cli-validator-2-1  Started 0.6s
  ✓ Development server started successfully
```

### Manage the services

The following commands can be used stop, check the status of, and view logs for the development environment, including the Bitcoin regtest network and Arch Network nodes.

```bash
arch-cli server status
```

The following is an example output from querying the server status.

```bash
Welcome to the Arch Network CLI
  → Loading configuration from /Users/jr/Library/Application Support/arch-cli/config.toml
Checking development server status...
  → Checking Bitcoin regtest network status...
    ✓ bitcoin is running
    ✓ electrs is running
    ✓ btc-rpc-explorer is running
  → Checking Arch Network nodes status...
    ✓ bootnode is running
    ✓ leader is running
    ✓ validator-1 is running
    ✓ validator-2 is running
```

We'll reference these later in the book. For now, familiarize yourself with starting and stopping the stack.

```bash
arch-cli server stop
arch-cli server logs [<service>]
```

Great, you're ready for hacking!

[arch-cli]: https://github.com/Arch-Network/arch-cli
[arch-docker-compose.yml]: https://github.com/Arch-Network/arch-cli/blob/main/arch-docker-compose.yml
[bitcoin-docker-compose.yml]: https://github.com/Arch-Network/arch-cli/blob/main/bitcoin-docker-compose.yml
[btc-rpc-explorer.dockerfile]: https://github.com/Arch-Network/arch-cli/blob/main/btc-rpc-explorer.dockerfile
