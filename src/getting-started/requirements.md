# Requirements

The following dependencies are needed to proceed. Install these before moving to the next step.

- [Rust](#install-rust)
- [Docker](#install-docker)
- [A C++ Compiler (gcc/clang)](#install-c-compiler)
- [Node.js v19+](#install-nodejs)
- [Solana CLI](#install-solana-cli)
- [Arch-cli](#clone-the-arch-cli-repository)

### Install Rust
First, to work with Arch programs you will need Rust installed on your machine. If you don't have it, you can find installation instructions on [the Rust website].

It is assumed that you are working with a stable Rust channel throughout this book.

### Install Docker
Next, Docker is required to run Arch's containerized node infrastructure locally. The desktop client can be installed from [the Docker website].

### Install C++ Compiler

For MacOS users, this *should* already be installed alongside [gcc] so you can skip this section.

For Linux (Debian/Ubuntu) users, this must be installed if it isn't already. We will manually install the [gcc-multilib].
```bash
sudo apt-get update
sudo apt-get install gcc-multilib
```

### Install Node.js

Please make sure you have [Node.js] version 19 or higher installed as [npm] is required to run the various front-ends within the repository. 

### Install Solana CLI

To compile the examples, the [Solana] CLI toolchain must be installed. Execute the following commands to install the toolchain to your local system.

#### MacOS & Linux

```bash
sh -c "$(curl -sSfL https://release.solana.com/v1.18.18/install)"
```

> You can replace v1.18.18 with the release tag matching the software version of your desired release, or use one of the three symbolic channel names: stable, beta, or edge. 
>
> Ref: [Solana Docs].

> ⚠️ **NOTE:** Installing [rust] through [Homebrew] likely leads to issues working with `cargo-build-sbf`. Below are some steps to get around this.

#### Steps:

1. Uninstall rust.
```bash
rustup uninstall self
```

2. Ensure rust is completely removed.
```bash
rustup --version

# should result:
zsh: command not found: rustup
```

3. Reinstall rust.
```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

4. Reinstall solana.
```bash
sh -c "$(curl -sSfL https://release.solana.com/v1.18.18/install)"
```

> If you are still experiencing errors, join our [Discord dev-chat] channel for more support.

### Clone and install the arch-cli

Finally, we'll be using a repository specifically made to demonstrate Arch's capabilities and get you started building quickly: `arch-cli`. 

The `arch-cli` [repo] provides a local Arch Network development environment, a command-line tool to setup new projects, deploy programs and more, as well as provides an example dapp to showcase Arch functionality that we will touch on later in this book. The `arch-cli` also ships with a mini block explorer for additional visibility into transactions and block production.

```bash
git clone https://github.com/arch-Network/arch-cli && \
cd arch-cli

# install
cargo install --path .
```

[GCC]: https://gcc.gnu.org/
[gcc-multilib]: https://packages.debian.org/sid/gcc-multilib
[npm]: https://github.com/npm/cli
[eBPF]: https://ebpf.io/
[repo]: https://github.com/arch-Network/arch-cli
[rust]: https://www.rust-lang.org
[Solana]: https://github.com/solana-labs/solana
[Node.js]: https://nodejs.org/en/download/package-manager
[Homebrew]: https://brew.sh/
[Solana Docs]: https://docs.solanalabs.com/cli/install#macos--linux
[the Rust website]: https://www.rust-lang.org/tools/install
[the Docker website]: https://www.docker.com/products/docker-desktop/
[Discord dev-chat]: https://discord.com/channels/1241112027963986001/1270921925991989268
