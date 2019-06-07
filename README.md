# ONC Plasma

## Plasma Application + Interoperability Research ⚡ (ONC PAIR) ⚡

***[Results of ONC Bounty #1:](https://forum.omgnetwork.org/t/request-for-information-onc-stewardship-over-cosmos-spoon/61)*** 

🔮 ⛓️ **CONNECTING PLASMA TO MULTIPLE ROOT CHAINS** ⛓️ 🔮

*ONC Multi-Root Plasma (ONC MRP)*

**Benefits:** 

> * Makes Plasma interoperable across many Layer 1 blockchain networks like Ethereum, Cosmos, Polkadot.
> * Utilizing this Layer 1 *bridge*, tokens can be used to indirectly execute contracts among different blockchain networks.

**Immediate Problems (Pending Research):**

> * Plasma withdrawal time of 2 weeks = bad UX.

**Design:**

REQUIREMENTS TO SATISFY - 

* Foundation requirements
> * Use the existing Tesuji plasma chain design.
> * Use the existing plasma contract design of OmiseGO, so that the plasma contract code can be used *as is* or can be used to program a duplicate contract code in each root chain.

* Core requirements
> * Support for multiple wallet addresses and private key schemes that each root chain uses.
> * Token transfers only within same root chain wallets (Ethereum, Cosmos, etc.).
> * Depositing and Withdrawing tokens, from and to different root chains.

* Integration requirements
> Must integrate well and support DEX across tokens from all the root chains.

**HIGH LEVEL DESIGN**

The existing plasma contract design/code of omisego is used to implement a duplicate plasma contract on the other root chain. E.g., *OMG Cosmos Zone*.

The overall design is to use root chain id and wallet types with the existing Tesuji plasma chain.

The UTXO output already holds the token, token amount, wallet address, etc.

Root chain id and wallet type needs to be additionally stored within the UTXO output.

Root chain id can be some unique three/four letter symbol to identify the root chain he token belongs to. 
E.g., *ZOMG for Cosmos OMG Zone*. This root chain id is added to the UTXO ouput.

Wallet types are for Ethereum, Cosmos, etc. The wallet type is added to the UTXO ouput. The wallet address in the UTXO output then corresponds to the wallet type. The wallet type is used to choose the transaction signing method. Given a private key, the wallet type is used to determine if the provided key matches with the wallet address. 

> Example wallet types are Ethereum ECDSA : uses ECDSA secp256k1 eliptic curve & Keccak256 hashing, Cosmos EDDSA : uses EDDSA ed25519 eliptic curve & SHA256 hashing, etc.

> For wallet type Ethereum ECDSA, a sample private key to wallet address matching.
> * STEP 1 : Public Key = ECDSA secp256k1(Private Key) -> converts private key to public key using ECDSA secp256k1.
> * STEP 2 : hash = Keccak256(Public Key) -> Convertes public key to hash using Keccak256 or SHA3 hashing function.
> * STEP 3 : Wallet Address = ‘0x’ + last 20 bytes of hash.

*Deposits, Withdrawals and Transfers*

> When depositing from a root chain, an UTXO is created with the corresponding root chain id, wallet type, wallet address, token, token amount, etc.

> When withdrawing an UTXO, the root chain id, wallet type, wallet address, token, token amount, etc. are used to exit. The root chain id is used to identify the root chain to exit to. The wallet type and wallet address provides the root chain wallet address to withdraw to.

> Token transfers are only done between wallets that have the same root chain id and wallet type.The wallet type is used to choose the transaction signing method. Given a private key, the wallet type is used to determine if the provided key matches with the wallet address.

*DEX across tokens from all the root chains*

Wallet A is from root chain 1 (e.g., *Ethereum, DAI*), Wallet B is from root chain 2 (e.g., *OMG Cosmos Zone, ATOM*):

> * User of wallet A, creates a wallet A1 in plasma chain, with root chain id belonging to root chain 2 (e.g., *OMG Cosmos Zone*);

> * User of wallet B, creates a wallet B1 in plasma chain, with root chain id belonging to root chain 1 (e.g., *Ethereum*);

> * User of wallet A sends chain1 token amount (e.g., *DAI*) to wallet B1. User of wallet B sends equivalent chain2 token amount to wallet A1 (e.g., *ATOM*).

*THE SUBSEQUENT TECHNICAL STEPS HERE ARE:*

**1.** Verify the above design from peers and make the necessary modifications.

**2.** Do the low level design or specification.

**3.** Implement and Test.

## Background Research Materials ⚡

### *What's Plasma, anyway?* 

#### ONC Resources

> * "[A short history of Plasma framework, what it is, where it’s going . . .](https://medium.com/coinmonks/a-short-history-of-plasma-framework-what-it-is-where-its-going-16920d0376a)" - **[Ro5s](https://medium.com/coinmonks)** - *[CoinMonks](https://medium.com/coinmonks)*


> * "[ELI5 OF PLASMA WHITEPAPER](https://medium.com/@tousthilagavathy/eli5-of-plasma-whitepaper-72e7570829a)" - **[Tousthilagavathy](https://medium.com/@tousthilagavathy/eli5-of-plasma-whitepaper-72e7570829a)**

_______________________________________________________________________________________________
👊 From [Open Network Community](https://forum.omgnetwork.org/) with ❤️
