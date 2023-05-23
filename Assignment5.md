Look at the example of init code in today's notes <br> Refer this gist: https://gist.github.com/extropyCoder/4243c0f90e6a6e97006a31f5b9265b94

## Q1. When we do the CODECOPY operation, what are we overwriting ?

> Based on the provided opcode, "CODECOPY" operation doesn't actually copy anything to the memory because the last paramater for the "CODECOPY" is the number of bytes to copy, but in this case, the total number of bytes specified are 0. So, no data is being overrided in the memory.

<hr />

## Q2. Could the answer to Q1 allow an optimisation ?

A. Yes, the code responsible for "CODECOPY" can be safely removed from the opcodes.

```
PUSH1 0xB6
DUP1
PUSH2 0x27
PUSH1 0x0
CODECOPY
```

<hr />

## Q3. Can you trigger a revert in the init code in Remix ?

> Yes. init code execution can be reverted just like a normal transaction execution. It can be reverted using "revert" keyword in Solidity.
In the context of the EVM bytecode, if the code encounters an INVALID opcode or runs out of gas during execution of the init code, it will also cause the transaction to revert.
An example can be sending ETH in the deploy transaction.

<hr />

## Q4. Write some Yul to

    - Add 0x07 to 0x08
    - store the result at the next free memory location.

A.

```
    assembly {
            let result := add(0x07, 0x08)
            let free_pointer := mload(0x04)
            mstore(free_pointer, result)
            free_pointer := add(free_pointer, 0x02)
            mstore(0x40, free_pointer)
        }
```

<hr />

## Q5. Can you think of a situation where the opcode EXTCODECOPY is used ?

A. EXTCODECOPY can be used for contract verification. When we want to verify if the bytecode at specific address matches a specific code, we can use EXTCODECOPY and fetch the code for further verification.

```
        function copyContractCode(address _addr) public view returns(bytes memory) {
            uint size;
            assembly{
                size := extcodesize(_addr)
            }
            bytes memory code = new bytes(size);
            if(size > 0){
                assembly {
                    extcodecopy(_addr, add(code, 0x20), 0, extcodesize(_addr))
                }
            }
            return code;
        }
```

<hr />

## Q6. Complete the assembly exercises in this repo: https://github.com/ExtropyIO/ExpertSolidityBootcamp

> Answers are pushed to my cloned repo: [CommitLink](https://github.com/dheeraj07/ExpertSolidityBootcamp/commit/3a1547d289c6fd7e3f5179519b61247f2c30fe00)
