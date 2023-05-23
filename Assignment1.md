## Q1. Why is client diversity important for Ethereum

> Client diversity is crucial for Ethereum as it ensures network security, robustness, and supports the principle of decentralization. The core principle of a public blockchain is decentralization So, to achieve that, client diversity plays a crucial role. It also provides choice for different user needs.

<hr>

## Q2. Where is the full Ethereum state held ?

> The entire history of the Ethereum state is held in archival nodes, while the current state is stored in both full nodes and archival nodes. Archival nodes maintain the full history of state changes, including every transaction and state change that has ever occurred on the Ethereum network. This is significantly more data than a regular full node.

<hr>

## Q3. What is a replay attack ? , which 2 pieces of information can prevent it ? 

> A replay attack is an exploit that can occur when two forked crypto-currencies allow transactions to be valid across both chains. A replay attack can copy an existing transaction from the new forked blockchain and make an identical one in the old blockchain (or the other way around).

> To prevent replay attacks: <br>
> 1. Nonce:  Transaction from a specific account has a nonce (a number that can only be used once). This number increases for each subsequent transaction. By checking this number, nodes can refuse transactions that use a nonce that's already been included in the blockchain, preventing replay attacks.
> 2. Chain ID: This is a unique identifier for a blockchain. Ethereum incorporated this into the transaction format after the Ethereum and Ethereum Classic split to prevent replay attacks between the two chains. By checking that the Chain ID in the transaction matches the Chain ID of the blockchain, nodes can prevent replay attacks from other chains.

<hr>

## Q4. In a contract, how do we know who called a view function ?
 
 > Since a view function doesn't modify the state of the blockchain, calling it doesn't require the user to have an Ethereum account, which makes it hard to determine who called the view function. As a workaround, we can pass an address parameter to the view function. Every time someone calls it, they can send their address as a function parameter, which allows us to identify who called it.