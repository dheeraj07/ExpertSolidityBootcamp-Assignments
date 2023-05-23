## Q1. Write a function that will delete items (one at a time) from a dynamic array without leaving gaps in the array. You should assume that the items to be deleted are chosen at random, and try to do this in a gas efficient manner. For example imagine your array has 12 items and you need to delete the items at indexes 8, 2 and 7.
The final array will then have items 0,1,3,4,5,6,9,10,11

A.

```
contract DeleteArray{
    uint public arr = [1,2,3,4,5,6,7,8];

    function deleteItem(uint index){
        require(index < arr.length, "Invalid index");
        arr[index] = arr[arr.length - 1];
        arr.pop();
    }
}
```
> Using "pop" is the best and most gas efficient way to completely remove an element from an array. Using "delete" sets the value at the specified index to its default value. In this case, using delete on an index sets the value at that index to 0, but it doesn't remove the index itself. The length of the array stays the same, and the index that was deleted still exists, but now contains a value of 0. 
The pop method is particularly efficient because it's a single operation that removes the last item, so it consumes the same amount of computational resources regardless of the size of the array.