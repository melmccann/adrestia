---
weight: 2
title: "Transactions and Balances"
date: 2020-05-26T07:53:51+01:00
---
# Transactions and Balances
In this section we will look at how to get an address balance, wallet balance and also the related transactions .


## Balance via Cardano Wallet

Cardano wallet allows us to get the combined address balance of all the wallets that we have:
```console
$ curl http://localhost:18090/v2/byron-wallets |jq

[
  {
    "passphrase": {
      "last_updated_at": "2020-06-24T13:12:18.682769651Z"
    },
    "state": {
      "status": "syncing",
      "progress": {
        "quantity": 0,
        "unit": "percent"
      }
    },
    "discovery": "random",
    "balance": {
      "total": {
        "quantity": 0,
        "unit": "lovelace"
      },
      "available": {
        "quantity": 0,
        "unit": "lovelace"
      }
    },
    "name": "MyByronTestnetWallet",
    "id": "9450c1d184dc0f8f9a27d8ddf3f69b3b1633e44d",
    "tip": {
      "height": {
        "quantity": 0,
        "unit": "block"
      },
      "epoch_number": 0,
      "slot_number": 0
    }
  }
]

```

#### List Wallet Transactions
```console
# cardano-wallet
$ curl http://localhost:8090/v2/byron-wallets/9450c1d184dc0f8f9a27d8ddf3f69b3b1633e44d/transactions
[
  {
    "inserted_at": {
      "time": "2020-05-26T10:30:36Z",
      "block": {
        "height": {
          "quantity": 1323322,
          "unit": "block"
        },
        "epoch_number": 61,
        "slot_number": 6871
      }
    },
    "status": "in_ledger",
    "amount": {
      "quantity": 2000000,
      "unit": "lovelace"
    },
    "inputs": [
      {
        "id": "100929648b7bac9c58830ac5b9e31bacc72ff180908586e37102c869c2a0477f",
        "index": 0
      }
    ],
    "direction": "incoming",
    "outputs": [
      {
        "amount": {
          "quantity": 2000000,
          "unit": "lovelace"
        },
        "address": "37btjrVyb4KEgngkooegdmhKTo8gpaprBgYepG9wpSRN14RAExiN3tfH7ENemtpAAfiJPBiCyY1uD9trYcqmGxyyMZCe1Xt4WwXYRdDoKdQbWzQemE"
      },
      {
        "amount": {
          "quantity": 1165898250,
          "unit": "lovelace"
        },
        "address": "37btjrVyb4KBvd49prUmRetJpgutzFB1TeuvoBwhp91NLTobYDJaDWVXBGkKtiFQa4cxV4ancnMCmrUqyk8YU7E86TC3sTArEoqmhijjYzKXpGrLAD"
      }
    ],
    "depth": {
      "quantity": 1,
      "unit": "block"
    },
    "id": "511f749c40f004de7d90495f43868289406d80a38f55cc4e40fe81e27ea5a4ea"
  },
  {
    "inserted_at": {
      "time": "2020-05-18T22:22:36Z",
      "block": {
        "height": {
          "quantity": 1290898,
          "unit": "block"
        },
        "epoch_number": 59,
        "slot_number": 17647
      }
    },
    "status": "in_ledger",
    "amount": {
      "quantity": 673305344,
      "unit": "lovelace"
    },
    "inputs": [
      {
        "id": "36d475c811f4ac4ab98d348387f5f91d14f1be86e0113359473bd5b2849a754e",
        "index": 0
      }
    ],
    "direction": "incoming",
    "outputs": [
      {
        "amount": {
          "quantity": 92791075064,
          "unit": "lovelace"
        },
        "address": "37btjrVyb4KCX6gMKnKUviWhUssrMNnb21jvBSevayrER6hLGfo6GZjRk4UfkwhAsbC14i28qjUDc3CSep6UoCUYNWCkgJ3E8RfgS2RuM9T7vYJbnX"
      },
      {
        "amount": {
          "quantity": 673305344,
          "unit": "lovelace"
        },
        "address": "37btjrVyb4KEgngkooegdmhKTo8gpaprBgYepG9wpSRN14RAExiN3tfH7ENemtpAAfiJPBiCyY1uD9trYcqmGxyyMZCe1Xt4WwXYRdDoKdQbWzQemE"
      }
    ],
    "depth": {
      "quantity": 32425,
      "unit": "block"
    },
    "id": "77c262193a7e2c77a63f038a91ad8321a423a9c6e4d542471ac582a2bc54bb42"
  }
]

```
It is worth noting that  `depth`.`quantity`, as seen in the transactions above, represents the number of "confirmations". Typically, in exchanges, this is checked and must pass a certain number of confirmations before funds are made available to the recipient.
```console
"depth": {
  "quantity": 1,
  "unit": "block"
},
```
This represents 1 confirmation.


## Balance via Cardano Rest Explorer Api

Here we will use cardano-rest to get address information.
If you have created an address offline (e.g. using cardano-addresses CLI) and do not wish to import it into cardano-wallet you should use this method for checking the "balance" and transactions of that address.

#### List Address Transactions & Balance

```console
# cardano-explorer-api
$ curl http://localhost:8100/api/addresses/summary/37btjrVyb4KEgngkooegdmhKTo8gpaprBgYepG9wpSRN14RAExiN3tfH7ENemtpAAfiJPBiCyY1uD9trYcqmGxyyMZCe1Xt4WwXYRdDoKdQbWzQemE

{
  "Right": {
    "caAddress": "37btjrVyb4KEgngkooegdmhKTo8gpaprBgYepG9wpSRN14RAExiN3tfH7ENemtpAAfiJPBiCyY1uD9trYcqmGxyyMZCe1Xt4WwXYRdDoKdQbWzQemE",
    "caType": "CPubKeyAddress",
    "caChainTip": {
      "ctBlockNo": 1333263,
      "ctSlotNo": 1334412,
      "ctBlockHash": "c26c4b40501151b45ffa98c5fd3163e2ab3df1caa34454f418e1d0d8fc3d24ee"
    },
    "caTxNum": 2,
    "caBalance": {
      "getCoin": "675305344"
    },
    "caTotalInput": {
      "getCoin": "675305344"
    },
    "caTotalOutput": {
      "getCoin": "0"
    },
    "caTotalFee": {
      "getCoin": "343767"
    },
    "caTxList": [
      {
        "ctbId": "77c262193a7e2c77a63f038a91ad8321a423a9c6e4d542471ac582a2bc54bb42",
        "ctbTimeIssued": 1589840556,
        "ctbInputs": [
          {
            "ctaAddress": "37btjrVyb4KDm6GkW7uBTr8ttH3XBCCrK57Vqamp4K5VeSPhaVYDSoUUmFbVdeZA1wWh3QWdFWdktDAzvmw29bJTP4SHCwJSoyXQn2dMiD5FHuv9xh",
            "ctaAmount": {
              "getCoin": "93464552665"
            },
            "ctaTxHash": "36d475c811f4ac4ab98d348387f5f91d14f1be86e0113359473bd5b2849a754e",
            "ctaTxIndex": 0
          }
        ],
        "ctbOutputs": [
          {
            "ctaAddress": "37btjrVyb4KEgngkooegdmhKTo8gpaprBgYepG9wpSRN14RAExiN3tfH7ENemtpAAfiJPBiCyY1uD9trYcqmGxyyMZCe1Xt4WwXYRdDoKdQbWzQemE",
            "ctaAmount": {
              "getCoin": "673305344"
            },
            "ctaTxHash": "77c262193a7e2c77a63f038a91ad8321a423a9c6e4d542471ac582a2bc54bb42",
            "ctaTxIndex": 1
          },
          {
            "ctaAddress": "37btjrVyb4KCX6gMKnKUviWhUssrMNnb21jvBSevayrER6hLGfo6GZjRk4UfkwhAsbC14i28qjUDc3CSep6UoCUYNWCkgJ3E8RfgS2RuM9T7vYJbnX",
            "ctaAmount": {
              "getCoin": "92791075064"
            },
            "ctaTxHash": "77c262193a7e2c77a63f038a91ad8321a423a9c6e4d542471ac582a2bc54bb42",
            "ctaTxIndex": 0
          }
        ],
        "ctbInputSum": {
          "getCoin": "93464552665"
        },
        "ctbOutputSum": {
          "getCoin": "93464380408"
        },
        "ctbFees": {
          "getCoin": "172257"
        }
      },
      {
        "ctbId": "511f749c40f004de7d90495f43868289406d80a38f55cc4e40fe81e27ea5a4ea",
        "ctbTimeIssued": 1590489036,
        "ctbInputs": [
          {
            "ctaAddress": "37btjrVyb4KCVShcCYDRXzgPtRBdtUmzt6GSzvUaULiStL2wPkPuPbxnD1GnewqZb2sEUfEa2Bi5pBtLuJm2w37k7rki7S3rgyB86LrUuwWtvQNK2j",
            "ctaAmount": {
              "getCoin": "1168069760"
            },
            "ctaTxHash": "100929648b7bac9c58830ac5b9e31bacc72ff180908586e37102c869c2a0477f",
            "ctaTxIndex": 0
          }
        ],
        "ctbOutputs": [
          {
            "ctaAddress": "37btjrVyb4KBvd49prUmRetJpgutzFB1TeuvoBwhp91NLTobYDJaDWVXBGkKtiFQa4cxV4ancnMCmrUqyk8YU7E86TC3sTArEoqmhijjYzKXpGrLAD",
            "ctaAmount": {
              "getCoin": "1165898250"
            },
            "ctaTxHash": "511f749c40f004de7d90495f43868289406d80a38f55cc4e40fe81e27ea5a4ea",
            "ctaTxIndex": 1
          },
          {
            "ctaAddress": "37btjrVyb4KEgngkooegdmhKTo8gpaprBgYepG9wpSRN14RAExiN3tfH7ENemtpAAfiJPBiCyY1uD9trYcqmGxyyMZCe1Xt4WwXYRdDoKdQbWzQemE",
            "ctaAmount": {
              "getCoin": "2000000"
            },
            "ctaTxHash": "511f749c40f004de7d90495f43868289406d80a38f55cc4e40fe81e27ea5a4ea",
            "ctaTxIndex": 0
          }
        ],
        "ctbInputSum": {
          "getCoin": "1168069760"
        },
        "ctbOutputSum": {
          "getCoin": "1167898250"
        },
        "ctbFees": {
          "getCoin": "171510"
        }
      }
    ]
  }
}


```
The array of transactions can be found under the key `caTxList`.
```console
"caTxList": [
  {
    ...
  },
  {
    ...
  }
]
```
The "balance" (UTXO) and fee information for the address can be seen in the following sections.
```console
"caBalance": {
  "getCoin": "675305344"
},
"caTotalInput": {
  "getCoin": "675305344"
},
"caTotalOutput": {
  "getCoin": "0"
},
"caTotalFee": {
  "getCoin": "343767"
},
```



## Sending Ada via cardano wallet

## Building Transactions with cardano-transactions

```console
cardano-tx empty 764824073 \
  | cardano-tx add-input 0 3b40265111d8bb3c3c608d95b3a0bf83461ace32d79336579a1939b3aad1c0b7 \
  | cardano-tx add-output 42 Ae2tdPwUPEZETXfbQxKMkMJQY1MoHCBS7bkw6TmhLjRvi9LZh1uDnXy319f \
  | cardano-tx lock \
  | cardano-tx sign-with 486fbdbe57d798bca3687151f861f82c6a042652a5e2ca4d90d8e221351ba647594cdedb4dbeec751e0b8ae3a5bc08c332f6748ab65ea61eaa6d913a6a7d5c4f33125f4592f303be5384bd8ead7a543b17c9f0707424edda0d992b705181fced \
  | cardano-tx serialize
```
Note that `764824073` is the mainnet tag for Byron.


### Transaction for sending Ada

### Transaction for storing Metadata Hash

### Transaction for Delegating Stake



## Submitting transactions via Cardano Rest Submit Api
