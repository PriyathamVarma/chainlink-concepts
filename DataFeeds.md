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
  
