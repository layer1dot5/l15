## Basic layer: Carrier Chain

L15 stands on three pillow:

* Lightning-like channels to control BTC (L15 lock-box)
* POW BTC merge-mined side-chain to record state (L15 side-chain)
* Threshold signatures for channels are made by randomly selected peers (L15vroutenode)

We re-implement BTC layer 2 after Lightning Network:

L15 is NOT intended to compete Lightning for fast and cheap payments. L15 is compliment to Lightning providing "DeFi" infrastructure whose assets may be then transferred by Lightning.

* Record a channel state into L15 side-chain
* Threshold Schnorr signatures and a random peer cluster as intermediary node, a new one for every channel
* Use PTLC for multi-hop payments for better privacy
* Extend state-channel protocol with DLC to connect to external world
* Better protocol implementation to not restrict its evolution and scaling

## Stable coin: L15$

Use Maker-DAO as predecessor:

* Collateral loan bases (using over-collaterisation)
* Service coin used as inflational asset to balance stable-coin price
* Auction-based collateral liquidation

Native to Bitcoin:

* BTC multi-sig channel as collateral lock-box with DLC-based end-of-terms (no any intermediary asset in between) DLC terms are recorded publicly at Side-chain ledger
* BTC-style - no any single account used to collect collaterals. Each collateral is locked in separate channel controlled by new random peer cluster

Next generation tokenomics model to provide better price referencing. (Can describe it as well but it is not my point of interest)

### BTC collateral release solution

Peers from signers' cluster are not good choice to control a collateral honey-pot. Their's role is just forward payments without ability to steal a value. They are main drivers of the system: sign if you can and get your fee. So they cannot take a decision to sign or not to sign - they sign always.

Collateral unlock has another nature: pay-off has to be signed in case appropriate amount of L15$ is burned:

* Directly by collateral owner
* As a result of collateral liquidation auction

Solution: Build DLC output transaction with special condition in its script:

* Anyone who provide an arbitrage bond can return the collateral back to DLC during some "enforcement" period

  * If this "return" was legal then the arbiter can atomically mint L15 service coin and exchange it into BTC (using embedded DEX) for amount of its bond + award. The go for the procedure is provided by miners and overall POW consensus
  * In case of illegal "return" no miners will allow to mint the above and arbiter will lost their bond… 

  Yes, the arbitrated trustless collateral unlock needs trustless DEX to be invented as part of L15 protocol. Anyway the same is needed for advanced tokenomics model!..

  As well we need to have at least BTC price oracle, it is better to be decentralized and hosted by L15 side-chain