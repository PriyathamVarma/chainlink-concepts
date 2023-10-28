# Data feeds

![Data feeds](https://github.com/PriyathamVarma/chainlink-concepts/blob/main/Images/Screenshot%202023-10-28%20at%2012.29.13.png)

- Get data and asset prices to smart contracts
- Premium data providers, aggregators and exchanges
- Various feeds

* Price feeds
* L2 sequencer uptime feeds
* NFT floor price feeds


Chainlink nodes ----> Smart contracts

- Each node can have its own source of information.
- Incentivised for running nodes


Basic price feed integration

```solidity
// This is for chainlink price feeds 
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.7;

// Imports
import "@chainlink/contracts/src/v0.8/interfaces/AggregatorV3Interface.sol";

contract priceFeeds{

    // Variables
    AggregatorV3Interface internal dataFeed;
    // This is the interface from chainlink, internal bcoz the data will be consumed by the contract only

    /**
     * Network: Sepolia
     * Aggregator: BTC/USD
     * Address: 0x1b44F3514812d835EB1BDB0acB33d3fA3351Ee43
     */

    // Constructor
    constructor(){
        dataFeed = AggregatorV3Interface(
            0x1b44F3514812d835EB1BDB0acB33d3fA3351Ee43
        );
    } 
    // Enums
    // Arrays
    // Maps
    // Modifiers

    // Functions
    function gettingDataFeedPrices() 
                public
                view 
                returns(int)
                {
                    (,int dataFromOracle,,,) = dataFeed.latestRoundData();

                    return dataFromOracle;
                }


}
```

Here are the methods for latestRoundData

```solidity
function latestRoundData() external view
    returns (
        uint80 roundId,
        int256 answer,
        uint256 startedAt,
        uint256 updatedAt,
        uint80 answeredInRound
    )

/*
Return values:

roundId: The round ID.
answer: The data that this specific feed provides. Depending on the feed you selected, this answer provides asset prices, reserves, NFT floor prices, and other types of data.
startedAt: Timestamp of when the round started.
updatedAt: Timestamp of when the round was updated.
answeredInRound:  Deprecated - Previously used when answers could take multiple rounds to be computed
*/
```

Useful resources:

1. [Data feeds api refrenece](https://docs.chain.link/data-feeds/api-reference)
  
