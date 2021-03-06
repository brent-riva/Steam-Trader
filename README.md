# Steam Trader

Implementation of a [Chainlink requesting contract](https://docs.chain.link/docs/create-a-chainlinked-project) created for the CoinList ChainLink hackathon. Thanks to Thomas and the CL team for the helpful Q&A in discord!

## Requirements

- NPM

## Installation

Clone this repo, then run:

```bash
npm install
```

Or

```bash
yarn install
```

## Test

```bash
npm test
```

## Deploy

If needed, edit the `truffle-config.js` config file to set the desired network to a different port. It assumes any network is running the RPC port on 8545.

```bash
npm run migrate:dev
```

For deploying to live networks, Truffle will use `truffle-hdwallet-provider` for your mnemonic and an RPC URL. Set these in the `.s/` folder (hidden and ignored from github; look in `truffle-config.js` to see what it looks for) or implement your own network setup in `truffle-config.js` file.

```bash
npm run migrate:ropsten
npm run migrate:mainnet
```

## Helper Scripts

There are 3 helper scripts provided with this box in the scripts directory:

- `fund-contract.js`
- `request-data.js`
- `read-contract.js`

They can be used by calling them from `npx truffle exec`, for example:

```bash
npx truffle exec scripts/fund-contract.js --network ropsten
```

The CLI will output something similar to the following:

```
Using network 'live'.

Funding contract: 0x972DB80842Fdaf6015d80954949dBE0A1700705E
0xd81fcf7bfaf8660149041c823e843f0b2409137a1809a0319d26db9ceaeef650
Truffle v5.0.25 (core: 5.0.25)
Node v10.15.1
```

In the `request-data.js` script, example parameters are provided for you. You can change the oracle address, Job ID, and parameters based on the information available on [our documentation](https://docs.chain.link/docs/testnet-oracles).

```bash
npx truffle exec scripts/request-data.js --network ropsten
```

This creates a request and will return the transaction ID, for example:

```
Using network 'ropsten'.

Creating request on contract: 0x972DB80842Fdaf6015d80954949dBE0A1700705E
0x828f256109f22087b0804a4d1a5c25e8ce9e5ac4bbc777b5715f5f9e5b181a4b
Truffle v5.0.25 (core: 5.0.25)
Node v10.15.1
```

After creating a request on a live network (ropsten, mainnet), you will want to wait 3 blocks for the Chainlink node to respond. Then call the `read-contract.js` script to read the contract's state.

```bash
npx truffle exec scripts/read-contract.js --network ropsten
```

Once the oracle has responded, you will receive a value similar to the one below:

```
Using network 'ropsten'.

21568
Truffle v5.0.25 (core: 5.0.25)
Node v10.15.1
```
