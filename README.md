// SPDX-License-Identifier: MIT
pragma solidity ^0.8.17;

contract ERC20 {
    // Total supply of the token
    uint public totalSupply;

    // Balances of token holders
    mapping(address => uint) public balanceOf;

    // Allowance mapping for delegated transfers
    mapping(address => mapping(address => uint)) public allowance;

    // Token details
    string public name = "Solidity by Example";
    string public symbol = "SOLBYEX";
    uint8 public decimals = 18;

    // Events for logging important token-related activities
    event Transfer(address indexed from, address indexed to, uint value);
    event Approval(address indexed owner, address indexed spender, uint value);

    /**
     * @dev Transfers tokens from the caller to a recipient.
     * @param recipient Address of the recipient.
     * @param amount Amount of tokens to transfer.
     * @return A boolean indicating the success of the transfer.
     */
    function transfer(address recipient, uint amount) external returns (bool) {
        require(balanceOf[msg.sender] >= amount, "Insufficient balance");

        balanceOf[msg.sender] -= amount;
        balanceOf[recipient] += amount;

        emit Transfer(msg.sender, recipient, amount);
        return true;
    }

    /**
     * @dev Approves a spender to spend a certain amount of tokens on behalf of the owner.
     * @param spender Address of the spender.
     * @param amount Amount of tokens to approve.
     * @return A boolean indicating the success of the approval.
     */
    function approve(address spender, uint amount) external returns (bool) {
        allowance[msg.sender][spender] = amount;

        emit Approval(msg.sender, spender, amount);
        return true;
    }

    /**
     * @dev Transfers tokens from one address to another, given the approval.
     * @param sender Address from which the tokens are transferred.
     * @param recipient Address to which the tokens are transferred.
     * @param amount Amount of tokens to transfer.
     * @return A boolean indicating the success of the transfer.
     */
    function transferFrom(
        address sender,
        address recipient,
        uint amount
    ) external returns (bool) {
        require(balanceOf[sender] >= amount, "Insufficient balance");
        require(allowance[sender][msg.sender] >= amount, "Insufficient allowance");

        allowance[sender][msg.sender] -= amount;
        balanceOf[sender] -= amount;
        balanceOf[recipient] += amount;

        emit Transfer(sender, recipient, amount);
        return true;
    }

    /**
     * @dev Mints new tokens and adds them to the caller's balance.
     * @param amount Amount of tokens to mint.
     */
    function mint(uint amount) external {
        balanceOf[msg.sender] += amount;
        totalSupply += amount;

        emit Transfer(address(0), msg.sender, amount);
    }

    /**
     * @dev Burns tokens, removing them from the caller's balance.
     * @param amount Amount of tokens to burn.
     */
    function burn(uint amount) external {
        require(balanceOf[msg.sender] >= amount, "Insufficient balance");

        balanceOf[msg.sender] -= amount;
        totalSupply -= amount;

        emit Transfer(msg.sender, address(0), amount);
    }
}

