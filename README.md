
QBFT Normal round (At system level)

1. Propose: The primary node proposes a new block and starts a timer. It sends a Pre-prepare message containing the block, current round number, and sequence number to all validators.
2. Pre-prepare: Validators receive the message. If valid, they store it and broadcast a Prepare message to all nodes, containing the current round number, sequence number, and block hash.
3. Prepare: Validators wait for Quorum (2N/3)  valid Prepare messages, including their own. If received within a timer limit, they move to the next step.
4. Commit: Validators send a Commit message containing the current round number, sequence number, and block hash to all nodes.
5. Finalize: After receiving Quorum (2N/3)  valid Commit messages, the block is finalized and added to the blockchain. The timer is reset.

   Timeout: If the timer expires at any point before finalization, validators increment the round number and proposer changes


Round change (Node level) 

1. Timer expiry triggers round changes message broadcast with current+1 round, any prepared round and corresponding value
2. At any time, if f+1 RC messages are received with round number higher than current , all valid, reset timer and set round number to min of those higher values, broadcast RC with the new round number and any prepared round - no justification needed here
3. Quorum of round change messages received for a round for which this node is proposer, and round change is justified, set value to highest prepared of this quorum if it exists or to input value.
4. Round change is justified if all RC messages have no PR and PV set or if there's a highest prepared round, that PR and PV should have corresponding Quorum of prepare messages

preprepare justification - first round or after a round change 
