// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

/**
 * @title ChainGuard Protocol
 * @notice A lightweight security and access-control contract template
 */

contract ChainGuardProtocol {

    address public owner;

    // Mapping to track approved guardians
    mapping(address => bool) public isGuardian;

    // Events
    event GuardianAdded(address indexed guardian);
    event GuardianRemoved(address indexed guardian);
    event OwnershipTransferred(address indexed oldOwner, address indexed newOwner);

    constructor() {
        owner = msg.sender;
    }

    // Modifier to restrict actions to the contract owner
    modifier onlyOwner() {
        require(msg.sender == owner, "Not authorized: Owner only");
        _;
    }

    // Modifier to restrict access to guardians
    modifier onlyGuardian() {
        require(isGuardian[msg.sender], "Not authorized: Guardian only");
        _;
    }

    /**
     * @notice Add a new guardian to the protocol
     * @param guardian The address to designate as a guardian
     */
    function addGuardian(address guardian) external onlyOwner {
        require(!isGuardian[guardian], "Already a guardian");
        isGuardian[guardian] = true;
        emit GuardianAdded(guardian);
    }

    /**
     * @notice Remove a guardian
     * @param guardian The guardian address to revoke
     */
    function removeGuardian(address guardian) external onlyOwner {
        require(isGuardian[guardian], "Address is not a guardian");
        isGuardian[guardian] = false;
        emit GuardianRemoved(guardian);
    }

    /**
     * @notice Transfer protocol ownership to another address
     * @param newOwner The new owner address
     */
    function transferOwnership(address newOwner) external onlyOwner {
        require(newOwner != address(0), "Invalid new owner");
        address oldOwner = owner;
        owner = newOwner;
        emit OwnershipTransferred(oldOwner, newOwner);
    }
}
contract address : 0x835B625cbB9E082787755a544619DB20a5e3960f
<img width="1349" height="258" alt="Screenshot 2025-11-27 104131" src="https://github.com/user-attachments/assets/0415d887-0deb-4689-be1e-e1728720b7a8" />

