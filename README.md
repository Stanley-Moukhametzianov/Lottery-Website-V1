# Lottery-Website-V1

* App uses react for the front end with web3 to make calls to the contract. 
* This contract is deployed on the Rinkeby test network at the address: 0xa1C447024f8F1cC189dDD96E6A0F1106C92Bd59C
* **Note:** Only the creator of the contract is able to activate the pick winner method. 


## :books: General info

* Users enter in an amount of test ether which must be greater than .01 ether. Then once the desired amount of players enter, 
the owner of the contract can call the pick winner function. This generates a pseudo random number which picks the winner. 
Then the balance of the contract is transfered to the winner. 
* **Note:** The winning number is not a true random number. It can be influnced and this contract should never be used in a real application. :D 



## :camera: Demo

![Demo](https://user-images.githubusercontent.com/66892566/147618600-33dc632b-1830-4fe8-8e8c-29396f69a40e.gif)


## :computer: Code Examples

* Lottery contract that is used in the website.

```solidity

pragma solidity ^0.4.17;

contract Lottery {
    address public manager;
    address[] public players;

    function Lottery() public{
        manager = msg.sender;
    }
    function enter() public payable{
        require(msg.value > .01 ether);
            players.push(msg.sender);

    }

    function random() private view returns (uint){
        return uint(keccak256(block.difficulty, now, players));
    }

    function pickWinner() public restricted {
        uint index = random() % players.length;
        players[index].transfer(this.balance);
        players = new address[](0);
    }
    modifier restricted(){
        require(msg.sender == manager);
        _;
    }

    function getPlayers() public view returns (address[]){
        return players;
    }

}

```


## :file_folder: License

* This project is licensed under the terms of the MIT license.

## :envelope: Contact

* Repo created by [Stanley Moukhametzianov](https://github.com/Stanley-Moukhametzianov?tab=repositories), email: stanleymoukh@gmail.com
