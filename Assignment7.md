## Q1. The parameter X represents a function. Complete the function signature so that X is a standard ERC20 transfer function (other than the visibility). The query function should revert if the ERC20 function returns false
A.
```
function query(
    address _to,
    uint _amount, 
    function(uint, address) external returns(bool) erc20)
    public 
    {
        require(erc20(_to, _amount), "Reverting the transaction");
    }
```

### How do we call the above function:

```
interface IERC20{
    function transfer(address _receiver, uint _amount) external returns(bool);
}

contract HelperCont{
    IERC20 tokenContract = IERC20(0XYTRDF56789.......);
    
    function initiateTransfer(address to, uint amount) public{
        query(to, amount, tokenContract.transfer);//calling the above function
    }
}

```
<hr />

## Q2. The following function checks function details passed in the data parameter.
```
function checkCall(bytes calldata data) external{ 
}
```
## The data parameter is bytes encoded representing the following:
```
    Function selector 
    Target address 
    Amount (uint256)
```
## Complete the function body as follows. The function should revert if the function is not an ERC20 transfer function. Otherwise extract the address and amount from the data variable and emit an event with those details
## event transferOccurred(address,uint256);

A.
```
function checkCall(bytes calldata data) external{
    require(bytes4(data) == bytes4(keccak256("transfer(address,uint256))), "Reverting the transaction");
    //bytes4 functionSelector = abi.decode(data[:4], (bytes4));
    (address Target, uint256 Amount) = abi.decode(data[4:], (address, uint256));
    emit transferOccurred(Target, Amount);
}
```
