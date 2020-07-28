# IBC Reporter

Nodejs app running on a server that scans all blockchans for events and handles IBC.

---
## Testnet setup

For the test environment both the 'EOS' and 'Telos pegger' tokens are created on the Telos test network. The environment required two sets on contracts (token contract and bridge contract), one for the EOS dummy contracts and on  for the Telos pegged tokens.

### EOSDT dummy token (EOS)

- Contract : eosdt.swaps
- IBC : eos.swaps

### EOSDT pegged token (Telos)

- Contract : usd.swaps
- IBC : issuer.swaps

---

## Setup

- Can be deployed on servers like any other NodeJS app.
- It's stateless and does not require any database.
- Requries Node.js

```bash
npm install
npm run build
# for production
npm start

# for testnets
npm run start-dev
```

The reporter requires environment variables to be set.
See `.template.env` - this file can be copied to `.env` and configured with the correct accounts and permissions.

```bash
# account name on EOS; permission used for reporting; private key for permission
EOS_IBC=maltareports;active;5JzSdC...
# ⚠️ Use your own endpoint here
EOS_ENDPOINT=https://eos.greymass.com
# same for TELOS
TELOS_ENDPOINT=https://api.telos.africa
TELOS_IBC=maltareports;active;5JzSdC...
```

#### Setup using Docker

Run the docker cotainer with your updated env file. Refer this template env file https://github.com/maltablock/eosdt-ibc/blob/master/reporter/.template.env-docker

``` docker run  --rm -it -v ${PWD}/env-commands:/env-commands aravindgv/eosdt:latest```

#### Different CPU payer

One can specify a different CPU payer for the actions run by the reporters.

```bash
# append cpu-account;cpu-key to the existing reporter;permission;key
EOS_IBC=maltareports;active;5JzSdC...;cpupayer;5k...
```

## Monitoring

There are some optional endpoints that can be used to check the health of the reporter, or a list of logs and performed transfer events.

A simple health check reporting the last checked block number on the chains can be seen on [/health](http://localhost:8080/health).

Logs can be seen on [/logs](http://localhost:8080/logs).
