# Foundry Template [![Open in Gitpod][gitpod-badge]][gitpod] [![Github Actions][gha-badge]][gha] [![Foundry][foundry-badge]][foundry] [![License: MIT][license-badge]][license]

A Foundry-based template for developing Solidity smart contracts, with sensible defaults.

## What's Inside

- [Forge](https://github.com/foundry-rs/foundry/blob/master/forge): compile,
  test, fuzz, format, and deploy smart contracts
- [Forge Std](https://github.com/foundry-rs/forge-std): collection of helpful
  contracts and cheatcodes for testing
- [PRBTest](https://github.com/PaulRBerg/prb-test): modern collection of
  testing assertions and logging utilities
- [Prettier](https://github.com/prettier/prettier): code formatter for
  non-Solidity files
- [Solhint](https://github.com/protofire/solhint): linter for Solidity code

## Getting Started

Click the
[`Use this template`](https://github.com/PaulRBerg/foundry-template/generate)
button at the top of the page to create a new repository with this repo as the
initial state.

Or, if you prefer to install the template manually:

```sh
mkdir my-project
cd my-project
forge init --template PaulRBerg/foundry-template
bun install # install Solhint, Prettier, and other Node.js deps
```

If this is your first time with Foundry, check out the
[installation](https://github.com/foundry-rs/foundry#installation)
instructions.

## Features

This template builds upon the frameworks and libraries mentioned above, so
please consult their respective documentation for details about their specific
features.

For example, if you're interested in exploring Foundry in more detail, you
should look at the [Foundry Book](https://book.getfoundry.sh/). In
particular, you may be interested in reading the
[Writing Tests](https://book.getfoundry.sh/forge/writing-tests.html) tutorial.

### Sensible Defaults

This template comes with a set of sensible default configurations for you to
use. These defaults can be found in the following files:

```text
├── .editorconfig
├── .gitignore
├── .prettierignore
├── .prettierrc.yml
├── .solhint.json
├── foundry.toml
└── remappings.txt
```

### VSCode Integration

This template is IDE agnostic, but for the best user experience, you may want
to use it in VSCode alongside Nomic Foundation's
[Solidity extension](https://marketplace.visualstudio.com/items?itemName=NomicFoundation.hardhat-solidity).

For guidance on how to integrate a Foundry project in VSCode, please refer to
this [guide](https://book.getfoundry.sh/config/vscode).

### GitHub Actions

This template comes with GitHub Actions pre-configured. Your contracts will be
linted and tested on every push and pull request made to the `main` branch.

You can edit the CI script in
[.github/workflows/ci.yml](./.github/workflows/ci.yml).

## Installing Dependencies

Foundry typically uses git submodules to manage dependencies, but this
template uses Node.js packages because
[submodules don't scale](https://twitter.com/PaulRBerg/status/1736695487057531328).

This is how to install dependencies:

1. Install the dependency using your preferred package manager,
   e.g. `bun install dependency-name`
   - Use this syntax to install from GitHub:
     `bun install github:username/repo-name`
1. Add a remapping for the dependency in [remappings.txt](./remappings.txt), e.g.
   `dependency-name=node_modules/dependency-name`

Note that OpenZeppelin Contracts is pre-installed, so you can follow that as
an example.

## Writing Tests

To write a new test contract, you start by importing
[PRBTest](https://github.com/PaulRBerg/prb-test) and inherit from it in your
test contract. PRBTest comes with a pre-instantiated
[cheatcodes](https://book.getfoundry.sh/cheatcodes/)
environment accessible via the `vm` property. If you would like to view the
logs in the terminal output you can add the
`-vvv` flag and use
[console.log](https://book.getfoundry.sh/faq?highlight=console.log#how-do-i-use-consolelog).

This template comes with an example test contract [Foo.t.sol](./test/Foo.t.sol)

## Usage

This is a list of the most frequently needed commands.

### Build

Build the contracts:

```sh
forge build
```

(If that does not show that the contracts are compiled/does not work, you
probably have the wrong forge, a snap package for Ubuntu installed. See
[solution](https://ethereum.stackexchange.com/questions/139754/when-i-type-forge-init-force-forge-init)
)

### Clean

Delete the build artifacts and cache directories:

```sh
forge clean
```

### Compile

Compile the contracts:

```sh
forge build
```

### Coverage

Get a test coverage report:

```sh
forge coverage
```

### Deploy

Deploy to Anvil, first open another terminal, give it your custom `MNEMONIC` as
an environment variable, and run anvil in it:

````sh
# This is a random generated BIP39 mnemonic seed with 0 test eth in it (on any
# network). To receive test eth you can ask Alchemy, which uses the test network:
# `ethereum-sepolia`. If you can get the faucet to give you test-ETH, you can use
# your own MNEMONIC (see [BIP39 mnemonic](https://iancoleman.io/bip39/).).
# [Their faucet](https://www.alchemy.com/faucets/ethereum-sepolia) keeps
# saying: "complete captcha", without showing the captcha (Add block was
# disabled).
```sh
export MNEMONIC="pepper habit setup conduct material wagon\
captain liquid ill confirm cube easy iron tackle timber"
````

I can not get test eth from the faucet, because captcha/alchemy does not like
privacy. (Test networks do not like privacy by design because otherwise the
test network can get (more easily) spammed).
Luckily foundry provides a standard test wallet with 1000 ETH in it, which can
be used with:

```sh
export MNEMONIC="test test test test test test test test test test test junk"
```

While Anvil runs in the background on another terminal, open a new terminal
and run:

```sh
forge script script/Deploy.s.sol --broadcast --fork-url http://localhost:8545
```

By default, this deploys to the HardHat Chain 31337.

For instructions on how to deploy to a testnet or mainnet, check out the
[Solidity Scripting](https://book.getfoundry.sh/tutorials/solidity-scripting.html)
tutorial.

### Format

Format the contracts:

```sh
forge fmt
```

### Gas Usage

Get a gas report:

```sh
forge test --gas-report
```

### Lint

Lint the contracts:

```sh
bun run lint
```

### Test

Run the tests:

```sh
forge test
```

Generate test coverage and output result to the terminal:

```sh
bun run test:coverage
```

Generate test coverage with lcov report (you'll have to open the
`./coverage/index.html` file in your browser, to do so simply copy paste the
path):

```sh
bun run test:coverage:report
```

## Related Efforts

- [abigger87/femplate](https://github.com/abigger87/femplate)
- [cleanunicorn/ethereum-smartcontract-template](https://github.com/cleanunicorn/ethereum-smartcontract-template)
- [foundry-rs/forge-template](https://github.com/foundry-rs/forge-template)
- [FrankieIsLost/forge-template](https://github.com/FrankieIsLost/forge-template)

## License

This project is licensed under MIT.

[foundry]: https://getfoundry.sh/
[foundry-badge]: https://img.shields.io/badge/Built%20with-Foundry-FFDB1C.svg
[gha]: https://github.com/TruCol/foundry-template/actions
[gha-badge]: https://github.com/TruCol/foundry-template/actions/workflows/ci.yml/badge.svg
[gitpod]: https://gitpod.io/#https://github.com/TruCol/foundry-template
[gitpod-badge]: https://img.shields.io/badge/Gitpod-Open%20in%20Gitpod-FFB45B?logo=gitpod
[license]: https://opensource.org/licenses/MIT
[license-badge]: https://img.shields.io/badge/License-MIT-blue.svg
