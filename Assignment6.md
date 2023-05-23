## Q1. Create a Solidity contract with one function: The solidity function should return the amount of ETH that was passed to it, and the function body should be written in assembly

A. 
```
function returnsSameValue() public payable {
        assembly{
            let result := call(gas(), caller(), callvalue(), 0, 0, 0, 0)
            if eq(result, 0){
                revert(0, 0)
            }
        }
    }
```

<hr />

## Q2. Do you know what this code is doing? https://gist.github.com/extropyCoder/9ddce05801ea7ec0f357ba2d9451b2fb


> The above opcode sequence creates two contracts. The first contract is created with the ETH value that was sent to the executing contract in the current transaction. The second contract is created without sending any ETH (0 value). The remaining ETH present in the current executing contract will be sent to the newly created contract (using the CREATE opcode a second time), and the current contract will be destroyed with the SELFDESTRUCT opcode.

<hr />

## Q3. Explain what the following code is doing in the Yul ERC20 contract.
```
function allowanceStorageOffset(account, spender) -> offset {
offset := accountToStorageOffset(account)
mstore(0, offset)
mstore(0x20, spender)
offset := keccak256(0, 0x40)
}
```

> The function "allowanceStorageOffset" in the provided code takes two inputs: the owner's account and the spender's account. It saves the owner's account at the 0x00 memory location and the spender's account at the 0x20 memory location. Both of these addresses occupy two complete 32-byte slots. The function then returns the Keccak-256 hash of 64 bytes starting from the 0x00 address up to the 0x40 address, where the owner's and spender's addresses are stored. This hashed value acts as the storage offset, which can be used to retrieve or update the token allowance for a particular (owner, spender) pair.