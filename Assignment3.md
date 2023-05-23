## Q1. What are the advantages and disadvantages of the 256 bit word length in the EVM?
A.

<B>Advantages:</B>
> Very useful for crypto primities for being compatible with cryptographic algorithms. For instance, Keccak-256 hash function (a variant of SHA-3) and secp256k1 elliptic curve used for generating Ethereum addresses both operate on 256-bit data.

<B>Disadvantages:</B>
> For operations that involve smaller data types, such as booleans, small integers, or individual bytes, the 256-bit word length can lead to unnecessary space wastage. This is because, when data is stored in memory, there is no data packing, so even smaller data types will occupy an entire 256-bit slot, even if it's not required.

<hr/>


## Q2. What would happen if the implementation of a precompiled contract varied between Ethereum clients ?
A.

> If the implementation varies between different clients, the results from execution calls could differ. This variation could halt consensus among the clients, causing them to end up with different versions of the Ethereum blockchain's state. This disagreement about the 'true' state of the blockchain could cause a network split, with some nodes following one version of the blockchain and others following a different version.


<hr/>

## Q3. Using Remix write a simple contract that uses a memory variable, then using the debugger step through the function and inspect the memory.
A.
![Remix screenshot](/remix.png)