# CreateAndMintERC20Token

This ERC20 token contract provides basic functionalities such as token minting, burning, and transferring, while adhering to the ERC20 standard. Customize and extend the contract further based on your specific project requirements and additional functionalities needed.

## Description

My project deals with the development of a custom ERC20 token, VAGToken, on the Ethereum blockchain. It provides basic functionalities of creation, burning, and transferring tokens. The token should be as flexible as possible to fit into a total of crowdfunding, decentralized applications, or even become a reward system in some ecosystem. It enables the minting of new tokens by the smart contract owner; it allows any users to burn their tokens, hence reducing the supply, and also conducts secure token transfers among others. It builds upon OpenZeppelin's libraries for ERC20 and access control, hence assuring reliability and security. This token would give any project the ability to support transactions and reward users for engagement in a fully decentralized manner.

## Getting Started

### Installing

To run this program, one can utilize the provided IDE for Solidity which is Remix. To access the website, please direct to this site [Remix IDE](https://remix.ethereum.org/)

Once you are on the website, create a new file on the "+" icon in the left-handed sidebar. Save the file with a `.sol` extension (e.g., `ERC20Token.sol`). Copy and paste the following code into the file:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.3.0/contracts/token/ERC20/ERC20.sol";
import "https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.3.0/contracts/access/Ownable.sol";

contract VladimirToken is ERC20, Ownable {
    constructor(uint256 initialSupply) ERC20("VAGToken", "VAGT") {
        _mint(msg.sender, initialSupply);
    }

    function mint(address to, uint256 amount) public onlyOwner {
        _mint(to, amount);
    }

    function burn(uint256 amount) public {
        _burn(msg.sender, amount);
    }

    function transfer(address to, uint256 amount) public override returns (bool) {
        _transfer(_msgSender(), to, amount);
        return true;
    }
}
```

To compile, click on the `Solidity Compiler` tab in the left-handed sidebar. Make sure the Compiler option is set to `0.8.26` (or another compatible version), and then click on the `Compile ERC20Token.sol` button.

Once the compiler does not return any errors, you can deploy the contract by clicking on the `Deploy & Run Transactions` tab in the left-hand sidebar. Select any account address that contains `100 ether`. Select the `Vladimir_Token` contract (e.g., `VladimirToken - ERC20Token.sol`) from the dropdown menu, and then click on the `Deploy` button. 

### Executing the program

Once the deployment is successful, you can proceed for a sample demonstration.

#### Imports
- Ensure that the import statements correctly point to the version of OpenZeppelin contracts (v4.3.0 in this case) that you intend to use.

#### Inherited Functions
- Functions like `_mint`, `_burn`, `_transfer` are inherited from `ERC20`, which provides core functionalities of an ERC20 token.

#### `Constructor (constructor(uint256 initialSupply) ERC20("VAGToken", "VAGT"))`
- Purpose: Initializes the contract with an initial supply of tokens minted to the address that deploys the contract `(msg.sender)`.
- Details: Calls the constructor of the ERC20 contract (from OpenZeppelin) with the token name "VAGToken" and symbol "VAGT". Mints initialSupply tokens to the deployer `(msg.sender)` using the `_mint` function inherited from ERC20.

#### `mint(address to, uint256 amount) public onlyOwner`
- Purpose: Allows the contract owner to mint new tokens and assign them to a specified address `(to)`.
- Details: `onlyOwner modifier` ensures that only the owner (deployer of the contract) can call this function. Calls `_mint` function from ERC20 to create amount tokens and assigns them to the address specified by `to`.

#### `burn(uint256 amount) public`
- Purpose: Allows any token holder to burn `(destroy)` their own tokens, thereby reducing the total supply.
- Details: `msg.sender` (the caller) specifies the amount of tokens (amount) they want to burn. Calls `_burn` function from ERC20 to reduce the balance of `msg.sende`r by amount tokens.

#### `transfer(address to, uint256 amount) public override returns (bool)`
- Purpose: Allows any token holder to transfer tokens from their own address to another address `(to)`.
- Details: `override` specifier is used to override the transfer function defined in ERC20. Transfers amount tokens from `_msgSender()` (the caller) to `to`. Calls `_transfer` function from ERC20, which handles the transfer logic and emits necessary events. Returns `true` if the transfer is successful.
  
## Help

If it somehow happens that `mint` does not perform, please review the Ethereum address. You can only mint tokens as the smart contract owner.

## Authors

Vladimir Al Guerrero
[@Linkedin](https://www.linkedin.com/in/vladimir-al-guerrero-178b6a24b/)

## License

This project is licensed under the MIT License - see the `LICENSE.md` file for details
