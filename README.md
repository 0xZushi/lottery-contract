# Lottery Contract
An Ethereum smart contract written in Solidity that holds lotteries.

>Users enter the lottery by purchasing a ticket. 1 ticket per address, no duplicates.
>
>Ticket fees are pooled into a pot. Winner takes all.
>
>Winner is randomly chosen once 100 tickets are purchased. After which a new lottery begins.
>
>Rinse and repeat.

### _Considerations:_
**Random winner**<br />Given that the blockchain is deterministic, we will produce the randomness off-chain via. an oracle.

### _Vulnerabilities:_
**Multiple entries by the same owner**<br />Given that the design of the lottery is to conclude upon the total purchase of 100 tickets in a cycle it is fairly easy for bad actors to increase their odds of winning by purchasing multiple tickets.<br />Possible solutions to remedy this are:
- **_Limiting the amount of tickets per address (currently implemented: 1 ticket per address)._** <br />This does not prevent the creation and ownership of multiple addresses to acquire additional tickets.
- **_Increasing the total tickets required to a large amount (e.g. 100000 tickets) before a cycle is concluded._**<br />This will drastically reduce the effectiveness of purchasing multiple tickets (i.e. ownership of 10 tickets provides a 10% chance of winning with 100 tickets vs. only 0.01% with 100000 tickets).
- **_Conclude the lottery based on a time interval._**<br />This would allow for an arbitary amount of tickets to be purchased before a cycle is concluded and therefore difficult for bad actors to gauge the effectiveness of their actions, this solution provides a similar effect to method above. Implementing this has its' own challenges as functions in Solidity can only be execeuted as part of a transaction so an off-chain app seems essential.
