// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

/**
 * @title BlockVerse Ledger
 * @dev A simple on-chain ledger for recording transactions and notes.
 */
contract Project {
    address public owner;

    struct Entry {
        uint256 amount;
        string note;
        uint256 timestamp;
    }

    Entry[] public entries;

    event EntryAdded(uint256 indexed id, uint256 amount, string note, uint256 timestamp);

    constructor() {
        owner = msg.sender;
    }

    /**
     * @dev Add a new ledger entry.
     * @param amount Amount to record.
     * @param note Description or note for the entry.
     */
    function addEntry(uint256 amount, string memory note) external {
        entries.push(Entry(amount, note, block.timestamp));
        emit EntryAdded(entries.length - 1, amount, note, block.timestamp);
    }

    /**
     * @dev Get a ledger entry by index.
     */
    function getEntry(uint256 index) external view returns (uint256, string memory, uint256) {
        require(index < entries.length, "Entry does not exist");
        Entry memory e = entries[index];
        return (e.amount, e.note, e.timestamp);
    }

    /**
     * @dev Return total number of entries in the ledger.
     */
    function totalEntries() external view returns (uint256) {
        return entries.length;
    }
}
