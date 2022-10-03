# 🪵 Yul Log 🪵

Yul Log is a package designed to serve as an easy to use unified toolchain for writing and using Yul+ Contracts. It's named after the dessert, partially to fit with Truffle's theme.

Yul Log reads from a directory called "Yul+ Contracts" within the local context, and expects only files with the .yulp extension inside. It will then compile your contracts and put the artifacts in ./artifacts/contracts for hardhat, and for truffle it will transpile them to Yul and put them in your contracts directory, then use truffle to compile it down to useable artifacts.

Right now Yul-Log works best with Foundry, for an example of the 2 together in action I reccomend checking out my [Yul+ Foundry Template](https://github.com/ControlCplusControlV/Foundry-Yulp).



## Installation

Simply install with node via

```
npm install -g yul-log
```

(sudo may be required depending on settings for a global installation)


After installing the package, run the following command to set up the development environment. 

```
yul-log init
```

Now you are all set up and can write `.yulp` files inside of the `Yul+ Contracts` directory.
or set YULP_CONTRACTS_DIR environment variable to use another directory
## Commands

```
yul-log
```

This will compile .yulp contracts inside of a "Yul+ Contracts" Directory in the current context into a hardhat artifact json file
unless you use 
```
yul-log !hardhat
```
which will output in the build directory in the following format
```
{
    "_format": "Yul+ Artifact Format v0.0.1",
    "contractName" : filename,
    "abi" : abi,
    "bytecode" : bytecode,
    "deployedBytecode" : deployedBytecode,
}
```

You can then use this json file however you would like in your current project.

```
yul-log truffle
```

This will compile .yulp contracts inside of a "Yul+ Contracts" Directory at the root of the project into truffle artifacts, which can then be treated like regular truffle contracts when testing. Note that if you are using truffle make sure the following is in your truffle-config.js

```
      solc: {
      version: "0.8.10",    // Fetch exact version from solc-bin (default: truffle's version)
      language : "Yul",
      // docker: true,        // Use "0.5.1" you've installed locally with docker (default: false)
        settings: {          // See the solidity docs for advice about optimization and evmVersion
        optimizer: {
          enabled: true,
          runs: 200
        },
```

so that you can compile Yul, as this will be used to compile the transpiled Yul, giving you more control over options and optimizations. After compiling the contract into truffle artifacts, you can run `truffle test` to run tests with truffle as normal.

```
yul-log hardhat
```
This will compile .yulp contracts inside of a "Yul+ Contracts" Directory at the root of the project into hardhat solidity artifacts (Use sig"" to remain compatible). Command is still very much a WIP, however it will generate a partial artifact that fits with a hardhat Solidity artifact, and can be treated similarly. However this isn't fully supported at the moment so expect issues and frequent manual fixes.
