# ERC20-Transfer-Fee-Send-Fee-to-Owner-
ERC20 Transfer Fee (Send Fee to Owner)
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

contract FeeToken is ERC20, Ownable {
    constructor() ERC20("FeeToken", "FEE") {
        _mint(msg.sender, 1000 ether);
    }

    function _transfer(address from, address to, uint256 amount) internal override {
        uint256 fee = amount / 100;
        uint256 sendAmount = amount - fee;

        super._transfer(from, owner(), fee);
        super._transfer(from, to, sendAmount);
    }
}
