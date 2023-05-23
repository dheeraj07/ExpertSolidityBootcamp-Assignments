## Q. Audit 1
Imagine you have been given the following code to audit:
[Contract](https://github.com/ExtropyIO/ExpertSolidityBootcamp/blob/main/exercises/audit/DogCoinGame.sol)

with the following note from the team

"DogCoinGame is a game where players are added to the contract via the addPlayer function, they need to send 1 ETH to play.

Once 200 players have entered, the UI will be notified by the startPayout event, and will pick 100 winners which will be added to the winners array, the UI will then call the payout function to pay each of the winners.

The remaining balance will be kept as profit for the developers," Write out the main points that you would include in an audit report.

## Audit Report: 
> 1. The players array does not need to be payable.
> 2. The numberPlayers variable should be incremented only when a player is successfully added.
> 3. The addPlayer function should include "require(msg.value == 1 ether)" statement to ensure that the player is sending the expected amount of ETH to participate.
> 4. The addWinner and payWinners functions should have appropriate access controls to prevent unauthorized users from modifying the winners array and paying out the winners.
> 5. In the payout function, the current balance check: "address(this).balance == 100" should be replaced with "address(this).balance >= 100" ether to ensure there's enough balance to pay out.
> 6. Before calculating amountToPay in the payout function, it's necessary to check if the winners array size is as expected (i.e., 100).
> 7. In the payWinners function, considering the numbers of players (200) and winners (100) are fixed, it might be more gas-efficient to hard-code the rewards instead of calculating it dynamically to avoid unnecessary overflows/underflows.
> 8. The payout function uses a loop to pay winners, which could potentially lead to a gas limit issue. It might be more efficient to allow winners to withdraw their rewards individually.
> 9. The contract seems to lack a method to withdraw the remaining balance after the winners payout, risking locking of funds in the smart contract.
> 10. In the payWinners function, use the transfer function instead of send to revert the transaction in case of any errors.
<hr>
