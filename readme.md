# pranavToken

This is a simple ERC-20 token contract implemented in Solidity. The contract allows for the creation and destruction of tokens, as well as checking errors through `require()`, `assert()` and `revert()` statements.

# Information 

simple explanation of the `require`, `assert`, and `revert` statements in Solidity:
* `require()`: The require statement is used to validate conditions within a smart contract. It is commonly used to check inputs or contract state before executing a function. If the condition specified in the 
              require statement evaluates to false, the transaction will be reverted, and any changes made to the state will be rolled back. It is often used for input validation, access control, and 
               preconditions. A custom error message can be included to provide more information about the error.
* `assert()`: The assert statement is used to ensure internal consistency within the contract. It is used to check for conditions that should never evaluate to false. If the condition specified in the assert 
              statement evaluates to false, it indicates a bug or an unexpected behavior in the contract. In such cases, the transaction will be reverted, and any changes made to the state will be rolled back.
* `revert`: The revert statement is used to trigger an immediate and deliberate reversal of a transaction. It is often used to handle exceptional situations or to revert a transaction explicitly with a custom 
            error message. When revert is called, the execution of the contract halts, and any changes made to the state are rolled back. It is useful for providing specific error messages or handling specific 
            error conditions within the contract. The error message passed to revert can provide details about the reason for the reversal.   

# Getting Started

### Requirements

 1. The contract has public variables that store the details about the coin:

    * `tokenName`:  A string representing the name of the token.
    * `tokenAbbrv`: A string representing the abbreviation of the token.
    * `totalSupply`: An unsigned integer representing the total supply of the token.


  2. The contract has a mapping of addresses to balances:

     * `balances`: A mapping that associates addresses with their corresponding token balances.

  3. The contract has a `mint` function that increases the total supply and the balance of the "sender" address by a given value:

     * Parameters :

       * `_address`: The address to which the tokens will be minted.
       * `_value`: The amount of tokens to be minted.
       *  `require` : pass the condition if condition true then move forward and minted token successfully otherwise shows an error message.
       *  `assert`: check the internal consistency within the contract that condition successfully act or not, if not then revert the token.

      * Actions :
    
       1. require condition fulfill or becomes true
        * Increase the `totalSupply` by `_value`.
        * Increase the balance of the `_address` by `_value`.

       2. require condition notfulfilled or becomes false
        * error msg displayed and transaction rollback


  5. The contract has a burn function that decreases the total supply and the balance of the "sender" address by a given value:

     * Parameters :

       * `_address`: The address from which the tokens will be burned.
       * `_value`: The amount of tokens to be burned.
       *  `revert`, `require` and `assert`

     * Actions :
       
        * if value <= 5 condition occur then `revert` statement true and shown an error msg 
        * Check the `revert` condition false then `require` condition fulfill in the below line condition define.
        * Check if the balance of the `_address` is greater than or equal to `_value` then move to another line of code if it false then shows an error msg
        * If true, decrease the `totalSupply` by `_value`.
        * Decrease the balance of the `_address` by `_value`.
          

### Usage

To run this program, you can use Remix, an online Solidity IDE. To get started, go to the Remix website at https://remix.ethereum.org/.


Once you are on the Remix website, create a new file by clicking on the "+" icon in the left-hand sidebar. Save the file with a .sol extension (e.g., pranavToken.sol). Copy and paste the following code into the file:

```javascript
// SPDX-License-Identifier: MIT
pragma solidity 0.8.18;

contract pranavToken {
    // public variables here
    string public tokenName = "Metaverse";
    string public tokenAbbrv = "MTS";
    uint public totalSupply = 0;

    /// mapping from user wallet address to token balance
    mapping (address => uint) public balances;

    
    function mint(address _address, uint _value) public {
        // Checking _value to be greater than zero or return the mentioned error message
        require(_value > 0, "Value must be greater than zero");

        totalSupply += _value;
        balances[_address] += _value;

        /* Assert that the balance of address has increased 
            by _value or returns the error if condition failed
        */
        assert(balances[_address] >= _value);
    }

    
    function burn(address _address, uint _value) public {
        if (_value <= 5) {
            revert("Value must be greater than five"); 
        }
        require(balances[_address] >= _value, "Insufficient balance"); // Require sufficient balance to burn

        totalSupply -= _value;
        balances[_address] -= _value;
           // Assert that the balance of address has decreased by _value or become 5
        assert(balances[_address] <= balances[_address] + _value);
    }
}

```

To compile the code,
Deploy the contract to an Ethereum network or use a development environment like Remix.

click on the "Solidity Compiler" tab in the left-hand sidebar. Make sure the "Compiler" option is set to "0.8.18" (or another compatible version), and then click on the "Compile pranavToken.sol" button.

Once the code is compiled, you can deploy the contract by clicking on the "Deploy & Run Transactions" tab in the left-hand sidebar. Select the "pranavToken" contract from the dropdown menu, and then click on the "Deploy" button.

Interact with the contract by calling the following functions:

* `mint`(address _address, uint _value): Mint new tokens and assign them to the specified `_address` parameter. The `_value` parameter must be greater than zero.

* `burn`(address _address, uint _value): Burn tokens from the specified `_address` parameter. The `_value` parameter must be greater than zero, and the `_address` must have sufficient balance.
      
## Authors

Pranav Shrivastava  
[@pranavshrivastava](https://www.linkedin.com/in/pranav-shrivastava-654817207)


## License

This contract is licensed under the MIT License. SPDX-License-Identifier: MIT.

