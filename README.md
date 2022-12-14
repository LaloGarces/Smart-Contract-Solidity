# Smart Contract Demo using Solidity ⟠ Ξ

## This is a demo to be used by both students and beginners in the world of Blockchain and Smart Contracts and, can learn all the components that Crypto transactions contemplate.

### We're going to use a real Smart Contract developed on Solidity. Thanks to professor Hadelin de Ponteves to share in one of his sessions the original code with me, attending one of his sessions. 

### We need the next ecosystems to interact with the Smart Contract: 

- Remix - Ethereum IDE: https://remix.ethereum.org/
- Ganache: https://trufflesuite.com/ganache/
- MyEtherWallet.com: https://www.myetherwallet.com/

In the case of My Ether Wallet, you can use the ZIP file uploaded in the repository. 

### Use the next code: 

You can personalize your own "Crypto" replacing Lalo Coins for the name of the coin you want. Remember, this is only a demo so the Cryptocurrencies created in this Smart Contract has value of $0 (In real life).

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

### Step 1
Once dowloaded Ganche and opened MyEtherWallet, please paste the code in Remix - Ethereum IDE.

On MyEtherWallet, select Add Custom Network/Node as in the next image: 

![This is an Image](https://github.com/LaloGarces/Smart-Contract-Solidity/blob/main/Screenshots/Step%201.png)

### Step 2
In the section *Set Up Your Custom Node*, please name your node as you wish and then use the URL and Port provided by Ganache. Then select ETH due, we're going to use that Crypto. 

![This is an Image](https://github.com/LaloGarces/Smart-Contract-Solidity/blob/main/Screenshots/Step%202.png)

### Step 3 
In MyEtherWallet, select *Deploy Contract* due we're going to seal the Smart Contract with the Genesis Block.

![This is an Image](https://github.com/LaloGarces/Smart-Contract-Solidity/blob/main/Screenshots/Step%203.png)

### Step 4
Within *Deploy Contract* you need to copy and paste the Byte Code from your Smart Contract. The Byte Code can be found within Remix: 

![This is an Image](https://github.com/LaloGarces/Smart-Contract-Solidity/blob/main/Screenshots/Step%205.png)

### Step 5
In the section *Paste your private Key* , use the Private Key provided by Ganache of the selected Account Addresss: 

![This is an Image](https://github.com/LaloGarces/Smart-Contract-Solidity/blob/main/Screenshots/Step%206.png)

### Step 6 
Sign Transaction and Deploy Contract.
![This is an Image](https://github.com/LaloGarces/Smart-Contract-Solidity/blob/main/Screenshots/Step%207.png)

### Step 7
In Ganche, you can see the Geneis Block for the creation of the contract. 

![This is an Image](https://github.com/LaloGarces/Smart-Contract-Solidity/blob/main/Screenshots/Step%2010.png)

### Step 8
Now, to start buying a Lalo Coin (you can rename it), within MyEtherWallet you need to select *Interact with Contract* and paste: 

- Contract Address: The address provided by your account within Ganache. 
- ABI: Your interface developed with Remix. Copy and paste it. 
![This is an Image](https://github.com/LaloGarces/Smart-Contract-Solidity/blob/main/Screenshots/Step%2012.png)

### Step 9
Then, within MyEtherWallet, select buy_lalocoins, copy your address from Ganache and, in the usd_invested select the amount of Lalo Coins you want to buy.

![This is an Image](https://github.com/LaloGarces/Smart-Contract-Solidity/blob/main/Screenshots/Step%2014.png)

### Step 10
Sign the transaction

![This is an Image](https://github.com/LaloGarces/Smart-Contract-Solidity/blob/main/Screenshots/Step%2015.png)

#Step 11
You can see in Ganache, your second Block mined!

![This is an Image](https://github.com/LaloGarces/Smart-Contract-Solidity/blob/main/Screenshots/Step%2016.png)

Thank you! 😊
