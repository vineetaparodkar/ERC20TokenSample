# ERC20 Overview

- ERC20 defines the functions balanceOf , totalSupply , transfer , transferFrom , approve , and allowance . 
- All of the previously described functionality is able to exist by defining a set of functions that allow a smart contract to emulate a digital token. 
- ERC20 fungible token standard
- A lot of these got released, and consequently, it was becoming hard to keep track of all these different standards of writing virtual currencies smart contracts on the network. Hence came in the proposal of ERC20 Standards
- This standardized how a token contract should look, resulting in the seamless integration of tokens in different protocols and crypto-wallets. The impact that ERC 20 therefore has on developers is massive, as projects do not need to be redone each time a new token is released. Rather, they are designed to be compatible with new tokens, provided those tokens adhere to the rules.
- "fungibility":  Fungibility is the ability of a good or asset to be readily interchanged for another of like kind. Think of two 1 dollar notes. Both the notes are different, but their value is exactly the same. The same is the case in an ERC20 token. Each token is worth the exact same as the other tokens in value.

- ERC:  Fungibility is the ability of a good or asset to be readily interchanged for another of like kind. Think of two 1 dollar notes. Both the notes are different, but their value is exactly the same. The same is the case in an ERC20 token. Each token is worth the exact same as the other tokens in value.. Each ERC is a set of rules and standards defined on top of the Ethereum blockchain and defines several things such as:
    smart contracts rules and conditions
    token creation rules
    token buy and sell conditions
    name and symbol of created tokens
    data standards
    wallets standards
    and more.

- EIP: Developers of the Ethereum community propose new standards for the Ethereum platform, by submitting an Ethereum Improvement Proposal (EIP). This includes protocol specifications and contract standards. Once that EIP is approved by a committee and finalized, it becomes an ERC.

- There are four types of standard EIPS:
Core: mentions or proposes changes to the EVM (Ethereum Virtual Machine)
Networking: improvements around transport protocols that are responsible for communication among Ethereum nodes (RLPx)
Interface: improvements around client API/RPC specifications and standards
Application: improvements around application or token level standards, e.g. ERC20
For this article, we will focus only on the application-level ERC standards.


## Overview of ERC20 functions

1. totalSupply()

- allows to calculate and return the total amount of the token that exists in circulation for a given ERC20 contract instance

- Since, it is labelled with a view modifier, calling it won’t consume any gas. So you can know about the total tokens in supply for any ERC 20 based token, for free. Zeppelin implements this logic by updating the value of internal variable totalSupply_ every time new tokens are minted.

2. balanceOf()

- This function return the balance of the provided address. The function accepts an address as a parameter, so it should be known that the balance of any address is public.

- Zeppelin maintains an internal mapping for this purpose, as follows:

    // Updated when tokens are minted or transferred

    mapping(address => uint256) balances;

3. approve()

- the owner of the contract authorizes, or approves, the given address to withdraw instances of the token from the owner’s address.

  // Create a table so that we can map

  // the addresses of contract owners to

  // those who are allowed to utilize the owner's contract

  mapping(address => mapping (address => uint256)) allowed;

4. transfer()

- it will consume gas, since it will result in a state change within the Ethereum Smart contracts. 

- This function lets the owner of the contract send a given amount of the token to another address 

5. transferFrom()

- This function allows a smart contract to automate the transfer process and send a given amount of the token on behalf of the owner.

- eg: Consider transferring money to pay a bill. It’s extremely common to send money manually by taking the time to write a check and mail it to pay the bill off. This is like using transfer() : you’re doing the money transfer process yourself, without the help of another party.
In another situation, you could set up automatic bill pay with your bank. This is like using transferFrom() : your bank’s machines send money to pay off the bill on your behalf, automatically. With this function, a contract can send a certain amount of the token to another address on your behalf, without your intervention.


Note: allowance, approve and transferFrom

 offer some advanced functionalities and are used to authorize some other Ethereum address to utilize your tokens on your behalf.
 This other Ethereum address could be a smart contract designed to handle tokens or just another account.

 Function approve is used by a token owner, to allow some spender to use a particular value of his tokens on his behalf.
Similarly, allowance can be used to check spender's allowance for a particular owner
And transferFrom can be finally used by spender to transfer allowed number of tokens.

The allowance() function takes in the address of the tokenOwner and the spender and gives as output, the number of tokens allowed to be transferred from a given address by another given address.
The transfer() function simply takes in the address of the receiver and the funds which are to be sent to the account. It then gives a boolean output value which is either true or false. True means that the amount was transferred successfully whereas false means the amount could not be transferred.
Then we have the approve() function. You can approve someone to spend from your account. This function takes the address of the spender along with the coins to be spent as the input and tells whether the transaction was a success or a failure.


- Approve: this allows you to give allowance to the user within the specified limit. Alice can call approve(bob,10). This allows Bob to have a 10 tokens allowance from Alice’s account; hence, Bob can take 10 tokens from Alice any time by calling transferFrom(alice, bob,10)

- transferFrom(from, to, amount): this allows users to move funds on behalf of the sender; if the sender gave allowance to the recipient with a specified amount, then the recipient can move the allowed amount on behalf of the sender

- allowance(sender, recipient): returns the amount of approved amount to the recipient address by the sender 

6. the _mint function creates new “amount” of token and increases the total supply. It assigns the new token to the “account” that is calling the function. This function is useful in order to mantain the synchronization between the totalSupply and the balance of the minted account (which increases by amount) and should always be used when increasing the total amount of an ERC20 token

7. the _burn() function is exactly the opposite of the _mint() function. In fact it is used in order to decrease the total supply of token. The amount of token will be burned from the account balance. When this operation is performed by developers, usually it results in a price increase of remaining tokens. The opposite is true for minting, which usually decreases the price of token.

8. Pausing
the ERC20PresetMinterPauser.sol contract, by inerithing from ERC20Pausable.sol, provides the pause() function which pauses all the token transfers until unpause() is called. This can be useful for scenarios such as preventing trades until the end of an evaluation period, or having an emergency switch for freezing all token transfers in the event of a large bug.



Advantages:

1. Higher chances of getting listed by exchanges.
2. Higher chances of integration with existing wallets.
3. This means your token can instantly be listed on exchanges and users can trade them with their existing wallets. Thus, it establishes interoperability.



Disadvantages:

1. Problem of lost tokens

    It happens during the transfer of ERC 20 tokens to a contract. When people mistakenly use the instructions for sending tokens to a wallet and send them to a smart contract which is not designed to handle it, their tokens get stuck in the smart contract. What’s worse? Since, the contract was not designed to handle these tokens, these tokens will be stuck there forever.

    If you send 100 ETH to a contract that is not intended to work with Ether, then it will reject a transaction and nothing bad will happen. If you will send 100 ERC 20 tokens to a contract that is not intended to work with ERC 20 tokens, then it will not reject tokens because it cant recognize an incoming transaction. As the result, your tokens will get stuck at the contracts balance.

    When you send a ‘non-compliant’ coin to the smart contract, the transfer function in that contract produces weird results like permanent loss of funds of the sender.
There is no warning to the user which says, “WARNING: if you send funds to this contract, they may be lost”, which should be there in this case.

Impossibility of handling incoming token transactions.
ERC20 has only functionality for moving and accounting for funds. There is no way to handle incoming token transactions and no way to reject any non-supported tokens. Tokens are simply credited to the receiver contract. Therefore, there is no way for the receiver to know about the credit and act upon the credited amount.


2. Reducing energy consumption

    The transfer of ERC223 tokens to a contract is a one step process rather than two steps process (for ERC20), and this means two times less gas and no extra Blockchain bloating.

3. If the code structure of all the tokens is different, then exchanges, wallets, smart contracts and other developers will have to write custom code to communicate with each type of token.
This will take a lot of time which means that for your token to be widely adopted, third parties would need a significant amount of time to change their code to support your token as well.

4. The batchOverflow Bug

    Simply put, this bug helped attackers to possess a lot of tokens out of nowhere.
    It is a ‘classical integer overflow issue.’ Here is a code snippet of the function that was faulty

5. The transfer process is inefficient.

    To transfer the tokens from account A to account B, users can call the transfer() function of the ERC20 token. For example, Alice can call transfer(bob.address,10). This method is suitable and safe for transferring to EOA (Externally Owned Accounts) only.
    However, if you want to transfer the tokens to the contract, you need to ensure that the receiver contract can handle the incoming transfers–that it is compatible with the ERC20 standard interface. An accidental token transfer to a non-ERC20 contract will result in a loss of tokens. If you transfer the tokens directly to a non-ERC20 contract, then the transfer will be successful, but the tokens are stuck forever in the receiver contract, since it doesn’t have the functionality to move the tokens from the contract.

    To send the funds to a smart contract, Alice needs to use the approve and transferFrom combination.
a. First, the user needs to set allowance for the receiverContract with an amount: approve(receiverContract,100)
b. Then, the user has to make a call from receiverContract to move user funds from the ERC20 token contract to the receiver contract using transferFrom(Alice,receiverContract,100)
c. This pattern is also gas-inefficient, since it requires two separate transactions to move the funds from the user to the receiver contract.

## References
1. https://medium.com/deqode/erc-token-standards-for-dummies-like-me-b6b8ace0f303

2. https://medium.com/blockchannel/the-anatomy-of-erc20-c9e5c5ff1d02

3. https://medium.com/coinmonks/all-you-need-to-know-about-erc-20-tokens-d7379e39b96f

4. https://medium.com/coinmonks/token-standards-erc20-vserc721-vs-erc1155-3106f1e3f2f3

5. https://medium.com/cryptoxtech/erc20-token-standard-a-beginners-guide-5b5f0c87e11f

6. https://medium.com/immunefi/how-erc-standards-work-part-1-c9795803f459 

7. https://medium.com/crypto-wisdom/erc-20-token-basics-for-crypto-beginners-231f988db36 

8. https://medium.com/coinmonks/my-first-erc20-token-7d5d16632818 

9. https://medium.com/@jgm.orinoco/understanding-erc-20-token-contracts-a809a7310aa5


## Additional notes

- ERC-20 is the one related to Token Standard. It is an “interface” that allows developers to build tokens on top of the Ethereum blockchain.

- In programming, an interface is the general description of a set of objects without declaring the behavior of objects.

- Let's review this with a simple example.
Imagine we have a general concept called “Vehicle”.
A motorcycle IS A vehicle.
A car is IS A vehicle.
A truck IS A vehicle.
Now, in order to describe a “Vehicle”, we may have these parameters or methods:
Example Properties
Clutch: the clutch property of the vehicle.
Brake: the brake property of the vehicle.
Seats: the seat property of the vehicle.
Example Methods:
Start: logic for starting the vehicle.
Stop: logic for stopping the vehicle.
Accelerate: logic for accelerating the speed in the vehicle.
Brake: logic for braking in the vehicle.
Now, motorcycles, cars, and trucks all share the same set of parameters and methods. However, each one of them may have its own version of implementation (functionality).
This is exactly where the term “interface” comes to play.
Interfaces define the abstract definition of the parameters and methods without defining the logic or implementation of them. Later on, each object can implement the interface and add its own version of the logic to it.

- ERC-20 is an interface powered by the Ethereum blockchain and using it, developers can build their customized tokens. In other words, ERC-20 is a set of abstract definitions of the properties and methods of a token. Later on, at the moment of implementation of an ERC-20 token, the developers can implement such properties and methods and add their own set of logic for their tokens.

- This standard is known as ERC20 which is basically a template, on the basis of which you can create your own token.
Think of MS Word or Google Docs. You can either create your own document or you can go with a template. Ethereum has the same ideology.
You can either create your own token from scratch or you can go with the ERC standard (template) to make changes according to your needs and customize your token the way you want.

- Decimals: The unit is used by smart contracts for accounting, as smart contracts work on integers, meaning that there can’t be any decimals. This unit is displayed to users (in any UI, from wallets to exchanges or any dApp). This is comparable to Ether, which uses 18 decimals for display. When showing 1080250000000000000000 for 18 decimals, it is much more user friendly to display it as 1'080.25 instead. Different tokens can opt for any decimals they want. USDC has 6 decimals, and USDT has 18 decimals. But by default, most ERC20 tokens choose 18 decimals.

What is its purpose?
Unfortunately, the solidity language and EVM does not support floating point number data-type: which means that all arithmetic operations in smart contracts happens between integers types. But what happens if you want to transfer 1.5 token? It is not possible in Solidity, so the EIP-20 Token Standard provides the decimals property, which defines how many 0s must be considered for the token.
For example, suppose an EOA wants to transfer 1.5 tokens to another EOA. In the user interface of the wallet it specifies the 1.5 tokens as the amount to transfer, but in reality the amount of token transferred is 1.5 * decimals. To be able to transfer 1.5 tokens, decimals must be at least 1, since that number has a single decimal place.
In OpenZeppelin decimals by default are set to 18, so when transferring 1.5 token, in reality the calculation is performed on 1.5*10¹⁸ = 1500000000000000000.


- What Is Token In Ethereum Network?
Tokens can signify virtually anything in Ethereum:
It can be a digital representation of any Fiat currency like USD
It can act as a lottery ticket
It can represent company equity shares
It can even represent digital gold & much more…
Now since it is such a great utility this token needs to have some rules and standards which can be extended and inherited, to be used by some other projects who may like to use the Ethereum blockchain platform. One such standard which is quite widely accepted by the Ethereum community is the ERC-20 standard.

- Characteristics of ERC -20 Tokens:
Every token which acts as a utility token to perform certain functions in the Ethereum network carries the following key attributes
They Are Fungible, which means every token should have the same code base, but they can be differentiated by their transaction history
As per Investopedia :
Fungibility is the ability of a good or asset to be interchanged with other individual goods or assets of the same type. Fungible assets simplify the exchange and trade processes, as fungibility implies equal value between the assets.
They are Transferable: Every token with ERC-20 standards can be easily sent or received on ERC-20 compatible addresses
They have a limited supply: Every token with ERC-20 standards are required to have a fixed supply threshold


- What Are Some Of The Prominent Use Cases Of ERC-20 Token Standard?
As a Transaction Fee: (Gas Fee):
There are multiple Defi and Dapps which are hosted on Ethereum Blockchain, to handle any transactions where one needs to give the fee(called Gas), these projects rely on their ERC-20 tokens which are held by the user in their wallet.
Act As a Digital Asset:
ERC-20 token can be used to represent multiple real-world properties like real estate, it can also represent art, music, stocks, physical hard drive, etc. In fact, it can represent physical gold in the digital form.
To Raise Funds(Crowdfunding ):
As an entrepreneur, if you are looking to crowdsource funds for your crypto or startups or any business for that matter, you can do so in the form of ERC-20 tokens. The investors get rewarded in the form of the newly minted tokens as initial coin offerings prior to the official launch
In Defi & Dapps :
ERC-20 based tokens are used on multiple Defi, Dapps, and business protocols
So the crux is that ERC-20 tokens act as one of the backbones of the Ethereum ecosystem, facilitating the development of multiple decentralized applications and popularizing the acceptance of the blockchain economy.
ERC-20 has been the key reason behind the widespread popularity & adaptation of decentralized technology by establishing a shared standard for participation in the blockchain world

## Improvements

ERC-223

ERC223 was introduced to fix major drawbacks in the ERC20 standard. It offers a solution to save token losses due to accidental transfers and gives the ability to receivers to accept or decline tokens arriving at their contract address. It no longer follows the (approve + transferFrom) ERC20 multistep standard to transfer the tokens to the contract. It is also a gas-efficient solution, as it requires a single transaction to transfer the tokens to the receiver contract.
ERC223 introduces a callback function for a receiving contract to handle the incoming tokens via the tokenReceived function. Users can now define a custom logic to accept or decline tokens arriving at their contact address using the tokenReceived function. If the recipient address doesn’t have a tokenReceived function, then the transaction will revert, preventing the accidental transfers to non-supported standard contracts which have plagued ERC20.


Now, the transfer() function has additional functionality which takes new optional argument data, which can be used to make a call to the recipient contract with the data supplied by the caller. The recipient contract can then use the supplied data to do something. This behavior also introduces the concept of transfer + call. This transfers the tokens and also instructs for something to be done on the recipient contract.
If the recipient address is a contract, then the ERC223 token makes a call to the recipient contract on tokenReceived function.

Drawback:

In the above code example, contracts can define their own logic to accept the incoming token transfer or to reject or many more.
The major drawback of ERC223 is that it overrides the design of transfer(address,uint256,bytes)function because it changes the behavior of standard ERC20’s transfer(address,uint256). It’s not backward compatible with existing ERC20 compatible contracts, since it always has a requirement of tokenReceived() function on the receiver contract; otherwise, the transfer will simply revert.


ERC-677

ERC677 aims to provide useful functionality without colliding with the ERC20 standard. This standard adds a new function transferAndCall() to the existing ERC20 standard, unlike the ERC223, which overrides the existing transfer() function.
transferAndCall() can be called to transfer tokens to a contract and then call the recipient contract with the additional data supplied by the sender. ERC677 tokens can be stored in any ERC20-compatible wallet. Receiving contracts could have the function onTokenTransfer(address,uint256,bytes) to write custom logic for the incoming call.

The major advantage ERC-677 has is that even if the recipient contract doesn’t have the onTokenTransfer() function, we can still use the regular ERC20 function transfer(address,uint256) to transfer the tokens. Hence the requirement of the dependent function on the recipient contract is optional. This makes it compatible with existing ERC20 tokens in space as we can use regular transfer() to transfer the tokens.

eg: One of the famous tokens which uses ERC677 is ChainLink (LINK) https://etherscan.io/address/0x514910771af9ca656af840dff83e8264ecf986ca#code

To do an API call or Chainlink VRF (Verifiable Random Function) request requires a function call on a smart contract. To do so, you also require a LINK token. With the regular ERC20 standard, you have to do it in multiple steps, e.g. (approve + call) on the contract. But using ERC677, you can do both in a single transaction transferAndCall(to,value,data). This first transfers the tokens to the receiver, then checks if the recipient is the contract, then makes a call on the recipient onTokenTransfer() along with the data.

The receiver contract checks if the incoming token call (msg.sender) is coming from the LINK address. Then it decodes the data supplied to the transfer and emits the RandomnessRequest event.

ERC-1363

ERC1363 does a similar thing to ERC677 but with some great extensions. In ERC677, we just had a transferAndCall() function, but EIP-1363 adds two more functions as extensions to the ERC677 with ERC20 standard compatibility.
transferFromAndCall(..) : Similarly to the transferAndCall(), the Receiver contract can now transfer the tokens from the spender to the receiver within the specified allowance limit and do something with a call.
approveAndCall(..) : Sets the allowance amount to the spender and do something with a call.
