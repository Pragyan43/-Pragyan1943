# Voting System

## Description

The VotingSystem smart contract facilitates a voting process where users can cast votes for candidates, and an owner can manage the election process. This contract is implemented in Solidity and can be deployed on the Ethereum blockchain.

## Getting Started
   # Features:
     1. Owner Management: Only the contract owner can add candidates and finalize the election.
     2. Voting Mechanism: Users can cast votes for candidates, with each user allowed to vote only once.
     3. Election Finalization: Once the owner finalizes the election, no more votes can be cast.
     4. Invariant Checks: Demonstrates the use of assert() to enforce invariants, ensuring that the election cannot be finalized without any votes cast.
     5. Error Handling: Uses revert() to handle invalid operations, such as attempting to vote multiple times.
   # Functions:
     1. vote(string memory candidate): Allows users to cast votes for a specified candidate.
     2. finalizeElection(): Allows the owner to finalize the election, marking it as completed.
     3. getVoteCount(string memory candidate): Retrieves the number of votes received by a specific candidate.
     4. checkInvariants(): Checks and asserts that certain conditions (like votes being cast before finalization) hold true.
     5. invalidFunction(): A function that always reverts with a predefined error message, showcasing error handling.
   # How to Use:
    1. Deploy the Contract: Deploy the contract using Remix or another Solidity development environment.
    2. Interact with Functions: Use different accounts to add candidates, cast votes, finalize the election, and check results.
    3. Explore Invariants and Error Handling: Test the contract's behavior under various scenarios to understand its functionality and robustness.Features:

### Executing program

To run this program, you can use Remix, an online Solidity IDE. To get started, go to the Remix website at https://remix.ethereum.org/.

Once you are on the Remix website, create a new file by clicking on the "+" icon in the left-hand sidebar. Save the file with a .sol extension (e.g., voting.sol). Copy and paste the following code into the file:

```javascript
pragma solidity ^0.8.13;

contract VotingSystem {
    
    address public owner;
    bool public electionFinalized;
    mapping(address => bool) public hasVoted;
    mapping(string => uint256) public votes;

    event VoteCast(address indexed voter, string candidate);
    event ElectionFinalized();

    constructor() {
        owner = msg.sender;
        electionFinalized = false;
    }

    modifier onlyOwner() {
        require(msg.sender == owner, "Caller is not the owner");
        _;
    }

    modifier notFinalized() {
        require(!electionFinalized, "Election has been finalized");
        _;
    }

    function vote(string memory candidate) public notFinalized {
        require(!hasVoted[msg.sender], "You have already voted");
        votes[candidate]++;
        hasVoted[msg.sender] = true;
        emit VoteCast(msg.sender, candidate);
    }

    function finalizeElection() public onlyOwner {
        electionFinalized = true;
        emit ElectionFinalized();
    }

    function getVoteCount(string memory candidate) public view returns (uint256) {
        return votes[candidate];
    }

    function checkInvariants() public view {
        
        if (electionFinalized) {
            assert(hasVotes());
        }
    }

    function hasVotes() internal view returns (bool) {
        for (uint256 i = 0; i < candidates.length; i++) {
            if (votes[candidates[i]] > 0) {
                return true;
            }
        }
        return false;
    }

    function invalidFunction() public pure {
        revert("This function is invalid");
    }

    string[] public candidates;

    function addCandidate(string memory candidate) public onlyOwner notFinalized {
        candidates.push(candidate);
    }
}


```

To compile the code, click on the "Solidity Compiler" tab in the left-hand sidebar. Make sure the "Compiler" option is set to "0.8.13" (or another compatible version), and then click on the "Compile voting.sol" button.

Once the code is compiled, you can deploy the contract by clicking on the "Deploy & Run Transactions" tab in the left-hand sidebar. Select the "VotingSystem" contract from the dropdown menu, and then click on the "Deploy" button.

Once the contract is deployed, you can interact with it by calling the getVoteCount function. Click on the "VotingSystem" contract in the left-hand sidebar, and then click on addCandidate and click transact to add the candidate name(e.g., "Pragyan").
Now by expanding the vote function under the deployed contract section, enter the candidate name (e.g., "Pragyan").Click the "transact" button to cast a vote.
You can switch accounts using the dropdown at the top of Remix to simulate different users casting votes.

Now click on finalizeElection function that allows the owner to finalize the election.

click on the "getVoteCount" function. Finally, click on the "call" button to execute the function and retrieve the number of votes.
Now Click on the "checkInvariants" function to check and assert that certain conditions (like votes being cast before finalization) hold true.
Then Click on the "invalidFunction" function that always reverts with a predefined error message, showcasing error handling.

## Authors

Metacrafter Chris  
[@metacraftersio](https://twitter.com/metacraftersio)


## License

This project is licensed under the MIT License - see the LICENSE.md file for details
