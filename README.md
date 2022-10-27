# Smart Contract Demo using Solidity ⟠ Ξ

## This is a demo to be used by both students and beginners in the world of Blockchain and Smart Contracts and, can learn all the components that Crypto transactions contemplate.

### We're going to use a real Smart Contract developed with Solidity. Thanks to professor Hadelin de Ponteves to share in one of his sessions the original code with me, attending one of his sessions. 

### We need the next ecosystems to interact with the Smart Contract: 

- Remix - Ethereum IDE: https://remix.ethereum.org/
- Ganache: https://trufflesuite.com/ganache/
- MyEtherWallet.com: https://www.myetherwallet.com/

In the case of My Ether Wallet, you can use the ZIP file uploaded in the repository. 

### Use the next code: 

You can personalize your own "Crypto" replacing Lalo Coins for the name of the coin you want. Remember, this is only a demo so the Cryptocurrencies created in this Smart Contract has value of $0

 ```
// SPDX-License-Identifier: UNLICENSED

// Lalo Coin & Smart Contract Demo

// Version of compiler
pragma solidity 0.8.7; 

contract lalocoin_ico {

    // Give the max number of Lalo Coins available when running the ICO (Initial Coin Offering)
    uint public maximum_lalocoins = 7000000;

    // Convertion rate from USD to Lalo Coins
    uint public usd_to_lalocoins = 700;

    // Show the total amount of Lalo Coins bought by the audience
    uint public total_lalocoins_bought = 0;

    // Mapping from buyers address to it's equity in lalo_coins and USD
    mapping(address => uint) equity_lalocoins;
    mapping(address => uint) equity_usd;

    // Validating if the new investors can buy Lalo Coins based on availability
    modifier you_can_buy_lalocoins(uint usd_invested){
        require (usd_invested * usd_to_lalocoins + total_lalocoins_bought <= maximum_lalocoins);
        _;
    }

    // Getting the equity in Lalo Coins of Investors
    function equity_in_lalocoins(address investor) external view returns (uint) {
        return equity_lalocoins[investor];
    }

    // Getting the equity in USD of Investors 
    function equity_in_usd(address investor) external view returns (uint){
        return equity_usd[investor];
    }

    // Buy Lalo Coins
    function buy_lalocoins(address investor, uint usd_invested) external
    you_can_buy_lalocoins(usd_invested) {
        uint lalocoins_bought = usd_invested * usd_to_lalocoins;
        equity_lalocoins[investor] += lalocoins_bought;
        equity_usd[investor] = equity_lalocoins[investor] / 700;
        total_lalocoins_bought += lalocoins_bought;
    }

    // Sell Lalo Coins
    function sell_lalocoins(address investor, uint lalocoins_sold) external {
        equity_lalocoins[investor] -= lalocoins_sold;
        equity_usd[investor] = equity_lalocoins[investor] / 700;
        total_lalocoins_bought -= lalocoins_sold;
    }
}
 ```
