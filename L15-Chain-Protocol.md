## L15 chain protocol

Version: 0

#### L15 Member (L15 Peer)

##### Defiintion

An **L15 Member** is an entity who confirmed knowledge of a private key corresponding to a public key, registered in the L15 chain. An L15 Member is uniquely identified by its public key.

#### The L15 Majordomo

##### Definition

**The L15 Majordodmo** is a set of L15 Members who confirmed hodling of a majority of L15SR coins and participating in peg-out validation. The L15 Majordomo can consist maximum of N (?) L15 Members who hodls largest L15SR deposits. The L15 Majordomo controls correctness of BTC peg out transactions and can collaboratively "roll back" an incorrect peg out transaction. ==?? Moreover, in case of absence of an action to roll back wrong peg out by exact, active for a particular contract, L15 Majordomo members can decide to use the bonds of failed members to bye back BTC to recover the stolen collateral (Do we need this or just mint new L15SR and sell it to recover the collateral?..).==

##### Requirements

1. First L15 Member, who receives block reward with the coinbase transaction of the block #0, becomes the L15 Majordomo immediately with no additional conditions.
2. Every next participant to the L15 Majordomo must
   1. publish his ==(M)== FROST nonce commitments,
   2. publish his VSS commitment share,
   3. publish signature of resulting aggregated VSS commitment, created with the participating key
   4. Send his L15SR bond to the new aggregated L15 Majordomo's address
3. In case there is just single participant in the L15 Majordomo when next participant appears:
   * if the first L15 Majordomo member is completed actions 2.1, 2.2, 2.3 then the new L15 Majordomo public key is FROST aggregated public key of first and second participants
   * if the first L15 Majordomo member is *not* completed actions 2.1, 2.2, 2.3 then
     * the new L15 Majordomo public key is the public key of the arriving participant
     * the first member still has an option to complete actions 2.1, 2.2, 2.3 to rejoin the L15 Majordomo public key
4. An member of the L15 Majordomo stops to play his role for newly created contracts if
   - he is not anymore in the list of N largest L15SR hodlers who already participate the L15 Majordomo
   - he has less then M published and unused FROST nonce commitments


Funds of the L15 Majordomo members have to be spendable:

1. By the member's public key and time locked for the whole period of contract duration. ==TBD: How to seamlessly extend the time lock? Possible introduce new consensus rule allowing spend a time locked output to the same key and with longer time lock even if initial lock hasn't timed out?==
   - Condition 1 is optional for the L15 Majordomo contained by first and single public key from the coinbase transaction of the block #0

2. By the aggregated key of all current L15 Majordomo members and the member's public key at any time

##### Specification

###### The L15 Majordomo Public Key

1. The L15 Majordomo Public Key is determined dynamically in time: it means it may change for every new contract according to the requirements listed above. However, once a contract is created at L15 chain, the L15 Majordomo public key remains same for the exact contract during the contract's lifetime.
2. The L15 Majordomo Public Key is secp256k1 EC public key aggregated according to FROST from The L15 Majordomo members' public keys which were actual at the L15 chain block where the contract was recorded.

###### The L15 Majordomo Address

1. The L15 Majordomo Address is Bech32m address according to Bitcoin TapRoot spec.
2. The L15 Majordomo Address is the L15 Majordomo Public Key as an Internal Public Key tweaked by a root of taptree scripts. The taptree contains a single script: the L15 Majordomo hodl script

``` <TBD: The L15 Majordomo hodl script>```

#### L15 Signer

##### Definition

An L15 Signer is an L15 Member who participates in L15 contract signing as part of virtual L15 counter-party. To become a signer, L15 Member has to commit a bond in Bitcoin to an L15 Majordomo controlled address. Particular signers are selected by the L15 Signer Selection Algorithm to sign a particular contract.

``` <TBD: An L15 Signer bitcoin deposit script>```

#### L15 Signer Selection Algorithm

##### Definition

