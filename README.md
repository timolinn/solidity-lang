# Solidity Docs

- A contract in the sense of Solidity is a collection of code (its functions) and data (its state) that resides at a   specific address on the Ethereum blockchain.

```solidity

pragma solidity ^0.4.0;

contract SimpleStorage {
    uint storedData;

    function set(uint x) public {
        storedData = x;
    }

    function get() public constant returns (uint) {
        return storedData;
    }
}```

- `uint` means unsigned integer.

- All identifiers (contract names, function names and variable names) are restricted to the ASCII character set. It is possible to store UTF-8 encoded data in string variables. But, Be careful with using Unicode text as similarly looking (or even identical) characters can have different code points and as such will be encoded as a different byte array.

- Coins are generated from contracts.

- You can generate a coin from thin air but only the person that created the contract can do that.

- Anyone can send coins to each other without any need for registering with username and password - all you need is an Ethereum keypair.

#### Simple cryptocurrency implementation

```solidity

pragma solidity ^0.4.0;

contract Coin {
    // The keyword "public" makes those variables
    // readable from outside.
    address public minter;
    mapping (address => uint) public balances;

    // Events allow light clients to react on
    // changes efficiently.
    event Sent(address from, address to, uint amount);

    // This is the constructor whose code is
    // run only when the contract is created.
    function Coin() public {
        minter = msg.sender;
    }

    function mint(address receiver, uint amount) public {
        if (msg.sender != minter) return;
        balances[receiver] += amount;
    }

    function send(address receiver, uint amount) public {
        if (balances[msg.sender] < amount) return;
        balances[msg.sender] -= amount;
        balances[receiver] += amount;
        Sent(msg.sender, receiver, amount);
    }
}
```
- `address` is a data type
