# Airdrop Smart Contract
This smart contract handles an airdrop event, allowing participants to register, play a game, and receive token rewards based on their performance. The contract integrates Chainlink's VRF (Verifiable Random Function) to ensure fairness in the random selection process.

## Features
- Registration: Users can register with a name to participate in the airdrop event.
- Game Participation: Registered users can participate in a game by making guesses. Random words are requested from Chainlink VRF.
- Result Calculation: Scores are calculated based on the user's guesses and the random words provided by Chainlink VRF.
- Prize Allocation: Users with high scores are marked for prizes. Winners are selected randomly from this pool.
- Airdrop Distribution: Tokens are distributed to all participants based on their status and scores.
- Claim Airdrop: Users can claim their airdropped tokens.

## Prerequisites
- Solidity ^0.8.7
- Chainlink VRF
- An ERC20 token contract for distributing the airdrop
- Contract Overview

## Imports
- VRFCoordinatorV2Interface: Interface for Chainlink VRF Coordinator.
- VRFConsumerBaseV2: Base contract for Chainlink VRF Consumer.
- IERC20: Interface for ERC20 tokens.
- Err.sol: Custom error definitions.

## State Variables
- owner: Address of the contract owner.
- erc20: ERC20 token contract address.
- COORDINATOR: Chainlink VRF Coordinator.
- NAME_MAX_LENGTH: Maximum length for participant names.
- winnersSelected: Indicates if winners have been selected.
- airdropDistributed: Indicates if airdrops have been distributed.
- keyHash: Chainlink VRF key hash.
- callbackGasLimit, requestConfirmations, numWords: Chainlink VRF parameters.
- s_subscriptionId: Chainlink VRF subscription ID.
- requestIds, allParticipants, prizes, winners: Arrays for storing request IDs and participants.
- Selection: Enum for HEAD/TAIL game guesses.
- Status: Enum for participant status (REGULAR, PRIZE, WINNER).
- RequestStatus, Participant: Structs for request status and participant details.
- mappings: Various mappings for participants, requests, balances, etc.

## Events
- GamePlayed
- RequestFulfilled
- Result
- Registered
- SelectWinners
- Airdrops
- ClaimAirdrop

## Modifiers
- onlyOwner(): Ensures that only the owner can call certain functions.

## Functions
### Constructor
- Initializes the contract with the Chainlink VRF Coordinator and ERC20 token contract addresses.
- Sets the contract owner.

## Private Functions
- checkAddressZero(): Reverts if the caller's address is zero.
- nameLength(string memory _name): Checks the length of a given name.

## Public/External Functions
- registration(string memory _name): Allows users to register with a name.
- userParticipateInGame(Selection[] memory _guesses): Allows users to participate in the game by making guesses.
- fulfillRandomWords(uint256 _requestId, uint256[] memory _randomWords): Called by Chainlink VRF with random words.
- getReturnedRandomNumbers(uint256 _requestId): Returns the random words for a given request ID.
- getParticipantResult(): Calculates and updates the participant's score based on random words.
- getParticipant(address _user): Returns the participant's details.
- selectWinnersFromPool(): Selects winners randomly from the prize pool.
- distributeAirdrops(): Distributes airdrops to all participants.
- getTokenBalance(): Returns the token balance for the caller.
- claimAirdrop(): Allows users to claim their airdropped tokens.

## Usage
- Deployment: Deploy the contract with the subscription ID and ERC20 token contract address.
- Registration: Users register using the registration function.
- Participation: Registered users participate in the game using the userParticipateInGame function.
- Results: Chainlink VRF provides random words. The contract calculates scores and updates participant status.
- Select Winners: The contract owner selects winners from the prize pool using the selectWinnersFromPool function.
- Airdrop Distribution: The contract owner distributes airdrops using the distributeAirdrops function.
- Claim Airdrop: Users claim their airdropped tokens using the claimAirdrop function.

## Error Handling
- The contract uses custom errors defined in Err.sol for various failure conditions such as address zero checks, name length validation, registration checks, and more.

## Events
- The contract emits various events to log significant actions such as game participation, request fulfillment, result calculation, registration, winner selection, airdrop distribution, and airdrop claims.

## Security
- Owner Only Functions: Certain functions are restricted to the contract owner using the onlyOwner modifier.
- Input Validation: Functions include checks for valid input to prevent misuse.
- Chainlink VRF: Ensures fair and verifiable random number generation for game results and winner selection.

## Author
### Michael Dean Oyewole

## License
- This project is licensed under the MIT License.
