## Q1. Why are negetive numbers more expensive to store than positive numbers?
## A
>All storage locations have zero value assigned on EVM. So, when changing from zero value to a non-zero value, more gas cost(20,000) is incurred than changing a non-zero value to non-zero value(5,000). Negative numbers are stored in the form of two's complement, which requires more '1' bits than a positive number. So, storing a negative number could be interpreted as costing more gas than storing a positive one, but it's critical to clarify that this isn't an intrinsic property of negative numbers costing more gas. It's more about the change in the state of storage – specifically, the change from zero to one, which incurs higher gas cost in Ethereum. 

>The EVM doesn't consider the individual bits of the values being stored when calculating gas costs, it is determined by the operation being performed, not the specific value being stored. The operation of storing a non-zero value in a storage slot that previously held a zero value is what triggers the 20,000 gas cost. This is true for both positive and negative numbers.

<hr>

## Q2. Test the following statements, and explain the reason which one is cheaper?
```
    1. result = numerator / demoninator;
    2. assembly { 
        result := div(numerator, demoninator)
        }
```

## A.
> In solidity, there are additional checks performed to prevent certain type of errors, hence the additional gas cost. Like, it checks for division by zero and automatically throws an error if denominator is zero.

> But, in the second statement, there are no validation checks are being performed, so if the denominator is zero, it might cause halt in the execution or some undesired result without returning the error. This absence of validations result in costing the lesser gas fees.