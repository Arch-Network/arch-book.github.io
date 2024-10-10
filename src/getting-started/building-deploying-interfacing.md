# Building, deploying and interfacing

Now that all of the dependencies are installed and we have successfully started our stack of development nodes, we can finally compile our program and interact with it.

`arch-cli` comes with an example dapp called GraffitiWall; each message written to the wall contains a timestamp, name and note.

Fortunately, the program was already compiled during the `arch-cli init` step which can be found from reviewing the previous logs.
```bash
...
Building Arch Network program...
...
```

### Build

If we wished to modify the program further before deploying, we would need to rebuild the program manually. If you do not wish to modify the program, skip this step and move to [Deploy].

Find the program's logic within the `src/app/program/src/lib.rs` file.

Access the `src/app/program/src` folder:
```bash
cd src/app/program/src
```

Build the program
```bash
cargo-build-sbf
```

This step will compile the example program into a [eBPF] ELF file, the executable format expected by the Arch VM.

You will find the generated shared object file at: `./target/deploy/arch_network_app.so`

_If you are experiencing issues with this step, we recommend returning to review the [requirements] page or hopping in our [Discord dev-chat] channel for support._

### Deploy
In this step, we will be submitting a transaction to store our program's logic on the Arch Network.

```bash
arch-cli deploy
```

Output:
```bash
Welcome to the Arch Network CLI
  → Loading configuration from /Users/jr/Library/Application Support/arch-cli/config.toml
Deploying your Arch Network app...
  ℹ Building program...
  ✓ Program built successfully
  ℹ Program ID: 3688ef8de06d56e32a765243e900875c4fefc6aa9c83dfbc2643f661c5b4982e
  ℹ Failed to load wallet 'devwallet'. Error: JSON-RPC error: RPC error response: RpcError { code: -18, message: "Wallet file verification failed. Failed to load database path '/home/bitcoin/.bitcoin/regtest/wallets/devwallet'. Path does not exist.", data: None }
Attempting to resolve the issue...
  ✓ Wallet 'devwallet' created successfully.
  → Generating initial blocks for mining rewards...
  ✓ Initial blocks generated
  ✓ Transaction sent: db69c08c4ff7df6081499d20c7f544f91f167fd184cbf3487f1ced8f1e75c848
  ✓ Transaction confirmed with 1 confirmations
    Creating program account...
    Program account created successfully
    Deploying program transactions...
Starting program deployment
  ℹ ELF file size: 175640 bytes
  → Deploying program with 210 transactions
  Transactions sent successfully                                                                                                                                             ✓ Successfully sent 210 transactions for program deployment
  [00:00:11] [########################################] 210/210 (100%)                                                                                                         Program transactions deployed successfully
    Making program executable...
    Transaction sent: 23de0a1d6fe6ec1f7304488aa223d092bcaa64ea63a23c61b765a248063e6e9c
    Program made executable successfully
  ✓ Program deployed successfully
  ✓ Wallet 'devwallet' unloaded successfully.
Your app has been deployed successfully!
  ℹ Program ID: 3688ef8de06d56e32a765243e900875c4fefc6aa9c83dfbc2643f661c5b4982e
  ```

Copy the Program ID from the output as you will need this again later. 

The Program ID can be thought of as a uniform resource locator (URL) for your deployed program on the Arch Network.

### Create an Account
An account is used to store the state for your dapp.

Obtain the Program ID from the deployment step output and use it within this command; you may need to replace this if the Program ID you received from the previous step differs from this one.

```bash
arch-cli account create --name graffiti --program-id 3688ef8de06d56e32a765243e900875c4fefc6aa9c83dfbc2643f661c5b4982e
```

Copy the Private Key from the output as you will need this when using the UI in the next step.

### Start the front-end application
```bash
arch-cli frontend start
```

Output:
```bash
Welcome to the Arch Network CLI
  → Loading configuration from /Users/jr/Library/Application Support/arch-cli/config.toml
Starting the frontend application...
  → Copying .env.example to .env...
  ✓ .env file created
  → Installing npm packages...
npm warn deprecated noble-secp256k1@1.2.14: Switch to namespaced @noble/secp256k1 for security and feature updates
npm warn deprecated @types/tailwindcss@3.1.0: This is a stub types definition. tailwindcss provides its own type definitions, so you do not need this installed.

added 393 packages, and audited 394 packages in 3s

131 packages are looking for funding
  run `npm fund` for details

2 vulnerabilities (1 moderate, 1 high)

To address all issues, run:
  npm audit fix

Run `npm audit` for details.
npm notice
npm notice New patch version of npm available! 10.8.2 -> 10.8.3
npm notice Changelog: https://github.com/npm/cli/releases/tag/v10.8.3
npm notice To update run: npm install -g npm@10.8.3
npm notice
  ✓ npm packages installed
  → Building and starting the Vite server...
  ✓ Vite server started
  → Opening application in default browser...
  ✓ Application opened in default browser
Frontend application started successfully!
Press Ctrl+C to stop the server and exit.
```

If the window doesn't pop up, navigate to: http://localhost:5173 to interface with your deployed program.

![](https://github.com/user-attachments/assets/6bad18c7-8523-454d-bbf4-d2e984c1d119)

Save your account's private key in the field in order to graffiti the wall and **refresh the page**.

🎨

Now you're ready to tag it!

[eBPF]: https://ebpf.io/
[Deploy]: #deploy
[requirements]: ./requirements.md
[Discord dev-chat]: https://discord.com/channels/1241112027963986001/1270921925991989268

