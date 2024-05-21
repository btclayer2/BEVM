# BEVM
## [An EVM-compatible Bitcoin Layer 2 with BTC as gas](https://github.com/btclayer2/BEVM-white-paper)

### Taproot Consensus is developed for the BEVM as part of the BTClayer2 technology suite. It parallels the ETHlayer2 Rollup technology solution in terms of its position and objectives.
The Taproot consensus is composed of three parts, combined to form a cohesive technical solution.
- The first part: Taproot technology, which includes Musig2, Schnorr signatures, MAST, and more.
- The second part: A BFT PoS network composed of Bitcoin SPVs.
- The third part: Threshold node communication formed through the Signal Protocol.

### What is Taproot?
Taproot is the most significant foundational framework upgrade for BTC since its introduction. It primarily comprises the following three BIPs:
- BIP340 (Schnorr signature): Schnorr's key aggregation feature allows participants of a single  multi-signature transaction to collaborate in combining their public keys, and produce an aggregate signature that is valid for the sum of their public keys. This saves block space, enhances privacy, and achieves faster transaction verification.
- BIP341 (Taproot): Bitcoin Improvement Proposal (BIP) 341 defines Pay-to-Taproot (P2TR), a new way of sending bitcoin. P2TR combines the functionality of Pay-to-Public-Key (P2PK) and Pay-to-Script-Hash (P2SH) scripts, giving users great flexibility and privacy benefits.
- BIP342 (Tapscript): Updates the script language used for writing BTC transaction parameters to accommodate users opting into the Schnorr and Taproot technologies.

### A BFT PoS network composed of Bitcoin SPVs
- 1. Bitcoin SPV: Bitcoin lightweight nodes, which do not require all BTC transactions, only need the block header and transactions interacting with layer2 to verify the validity and correctness of transactions.

- 2. BFT PoS Network: Utilizes a Substrate blockchain framework that combines Aura block production consensus and Grandpa BFT consensus.

### How does BEVM design Taproot Consensus?
#### Taproot Consensus nodes
Taproot Consensus nodes are primarily Bitcoin SPV nodes, which are then elected as Taproot Consensus nodes through governance voting by the entire network of BTC/BEVM stakers, ensuring the security of Taproot Consensus node elections through the safety of Layer2 BFT PoS consensus.

#### The Design of Taproot Consensus
Taproot consensus nodes combine Musig2 and the Signal  protocol to form decentralized on-chain threshold signatures that interact with the Bitcoin mainnet. Musig2 is a threshold signature scheme based on Taproot's security. The Signal protocol integrates the Double Ratchet Algorithm, pre-keys, and a three-pass Elliptic Curve Diffie-Hellman (3-DH) handshake, and uses Curve25519, AES-256, and HMAC-SHA256 algorithms as cryptographic primitives. It is currently the most secure communication protocol, addressing the security of communication between participants in Musig2's multi-party threshold signatures.

Musig2 ensures the security and flexibility of Bitcoin's threshold signatures, while the Signal protocol secures the communication of Taproot consensus nodes' threshold signatures. Bitcoin SPV nodes ensure the decentralization of Taproot threshold signatures, and the BFT PoS consensus of the BEVM layer2 network ensures the on-chain security of the Bitcoin SPV network.

***Taproot Consensus creates a decentralized #BTClayer2 solution by integrating Bitcoin's native Taproot technology stack with a BFT PoS network composed of Bitcoin SPV nodes.***

### Technical features:
- ***EVM:*** Fully compatible with EVM ecology, wallets such as metamask, development frameworks such as truffle/hardhat, and solidity programming language.
- ***BTC native gas:*** Use native BTC as the gas fee for EVM. Similar to ETH layer2 OP/Starknet, ETH is used as the gas fee of Layer2.
- ***Taproot Threshold Signature:*** On-chain POS nodes to ensure the decentralization of threshold signature verifiers. singal privacy communication protocol to ensure the security of the aggregated schnorr signature pubkey/msg.
- ***bitcoin light node:*** Light nodes on the BTC chain that support the Wasm version (no_std).
- ***Signal Privacy Distributed Protocol:*** [Signal protocol](https://en.wikipedia.org/wiki/Signal_Protocol) to ensure the privacy and security of message communication between nodes when schnorr aggregate signature and Mast contract combined threshold signature. 
- ***zkstark ultra-light node:*** To optimize the light nodes mentioned above, zkstark technology can be used to realize the ultra-light nodes of BTC.

### Four advantages compared to other layer2/cross-chain bridges （Take [tBTC](https://www.thresholdusd.org/en/) as an example）
- 1, ***No centralized initial setup required.*** There is no need to use sharding private keys to implement distributed threshold signatures, which avoids the security problem of private key leakage caused by sharding private keys.  Directly use BTC's native threshold signature scheme: [MuSig2](https://eprint.iacr.org/2020/1261).
- 2, ***Distributed network on the chain, more decentralized.*** The validators of the distributed threshold network are all block verification nodes on the chain, and the network on the chain increases trust. It avoids the opaque and easy-to-operate defects of the distributed network under the chain.
- 3, ***No permission required, just trust the code.*** The BTC to Layer2 network uses BTC light nodes. The blockchain logic of fully trusting the code avoids the centralized fraud problem caused by the submission of data oracle to the distributed network under the chain.
- 4, ***Distributed network communication with complete privacy.*** The [Signal protocol](https://en.wikipedia.org/wiki/Signal_Protocol) is used to complete the communication problem of the BTC taproot threshold signature. Solve the privacy communication problem of distributed network. Avoid the risks of data leakage, collusion or external attacks when threshold signatures appear

### EVM system with BTC as native Gas
#### The benefits of BTC as native Gas
- The largest BTC ecology, which is convenient for BTC users to hold BTC and use Layer2.
- BEVM's Sequencer can charge BTC fees to motivate BEVM Sequencer nodes.

#### BTC is compatible with EVM system
- BTC needs a Turing-complete smart contract platform to settle assets issued on BTC and BTC.
- The EVM ecology occupies more than 90% of the smart contract ecology in the market, and the compatible EVM ecology can accommodate the most expensive on-chain developers and user communities.

#### Technical realization
- Adopt substrate frame
- Precompiled system contracts, using BTC as gas
- Porting EVM platform

### Taproot Threshold Signature
Musig2 is a multi-signature protocol that only needs two rounds of communication to complete communication. It is a continuation and upgrade of Musig, and its practicability is greatly improved. This repo fully reproduces the multi-signature scheme proposed by [Musig2](https://eprint.iacr.org/2020/1261) Paper which the version is `20210706:150749`.At the same time, we implemented versions for secp256k1 and sr25519, respectively, so that we can use the Musig2 protocol in BTC  and Polka.

<img width="800" alt="WechatIMG475" src="https://github.com/btclayer2/BEVM/assets/9285062/a1e76f9f-0e9a-4cfc-9f43-ad0c8f51b619">

## Contribution
Any kinds of contribution are highly welcome. Feel free to submit an issue if you have any question or run into any issues.

## Metamask config for BTC
```
Network name: BEVM Canary network
RPC URL: https://rpc-canary-1.bevm.io
Chain ID: 11501
Currency symbol: BTC
Block explorer URL (Optional): https://scan.bevm.io/
```

## License

[GPL v3](LICENSE)

# References

- [schnorrkel](https://github.com/w3f/schnorrkel)
- [multi-party-schnorr](https://github.com/ZenGo-X/multi-party-schnorr)
- [musig2](https://eprint.iacr.org/2020/1261)

