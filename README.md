# DMix++

## Intoduction

In the beginning there was [DMix](https://fadibarbara.it/papers/dmix.pdf). It was a protocol acting as a decentralized mixer. We want to obfuscate Bitcoin transactions. Which is legal in any country, since arguably it does not provide any major improvement with respect to privacy. No need to [jail us](https://coingeek.com/tornado-cash-developer-must-stay-in-jail-for-3-months-dutch-judge-rules/), the point is to use cryptography cleverly.

## How DMix works

Alice has 1btc, Bob has .5btc and Carol has .25btc. They want to mix them. They do it in two steps.

### First step: funds pooling

Alice, Bob and Carol create a public key using a decentralized key generation (DKG) algorithm. we may call di pubkey `DMpub`: note that there is no `DMpriv`, since the key generation is decentralized, but there are *shares* of the private key. Alice owns `DMprivA`, Bob owns `DMprivB` and Carol owns `DMprivC`. 

Every user sends a transaction that can be spent using a transaction that has a signature with `DMprivA`, `DMprivB` and `DMprivC` before a certain time. After that time, the transaction can be spent by the user himself (see e.g. [here](https://github.com/bitcoin/bips/blob/master/bip-0112.mediawiki#Escrow_with_Timeout) for a construction). This transaction is called a *deposit transaction* for the user. There are as many deposit transactions as there are users.


### Second step: funds redeeming

TBD


## New Features

### Confondo
TBD

### PSU

The old protocol made Alice Bob and Carol reveal their new addresses to each other. What if Bob is malicious? He could tell external parties the new addresses of Alice and Carol. That would be a problem since it would allow other people to track the transactions invalidating the privacy of the protocol.

To mitigate this problem we propose to use Private Set Union (PSU). Private set union is a cryptographic primitive that let users compute the union of their input datasets without revealing any more information than the result. In our case, the input datasets are the new addresses of the users. The result is the set of new address for the redeeming of the pooled funds.

