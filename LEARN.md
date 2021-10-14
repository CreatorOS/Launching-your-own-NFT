# Launching your own NFT
Welcome to this quest! Here you will learn what an NFT is and how to launch your own.

__Subquest 1: Tokens, ERC20s and NFTs__

In the Ethereum network, there is the main currency called Ether. This currency is used as money, and it is also used to pay for network fees when you want to make transactions on the network.

Besides Ether, the Ethereum network allows you to create any number of sub-currencies known as tokens. These tokens are created by means of a smart contract that handles balances and sending tokens from one address to another. These tokens are written using the ERC-20 standard and you can find a detailed explanation on another quest. One of the main characteristics of these tokens is that they are fungible, which means that you cannot distinguish one token from another, only count them. These tokens are useful for all kinds of money-related applications.

Besides ERC-20, there exist in the Ethereum network another kind of token which are called Non-Fungible Tokens or NFTs for short.  An NFT or Non-Fungible Token is a __unique token__, which is also managed by a Smart Contract running in the Ethereum Blockchain. They are built using the ERC-721 standard.

__Subquest 2: Build and deploy your own ERC-721 Token using remix. __

Now we are going to deploy our own ERC-721 token inside a virtual environment using Remix.

There are two variables that need to be defined, they are the name and symbol of the token.

Please open [https://remix.ethereum.org/](https://remix.ethereum.org/)

We are going to use OpenZeppelin’s implementation of ERC-721 as the basis of our contract.

Let’s create a new file with .sol extension (for example, MyNFT.sol) and paste the following code:

// SPDX-License-Identifier: MIT

pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";

import "@openzeppelin/contracts/utils/Counters.sol";

contract MyNFT is ERC721 {

	using Counters for Counters.Counter;

	Counters.Counter private _tokenIdCounter;

    

    // URIs mapping

    mapping(uint => string) private _uris;

   constructor(

    	string memory name,

    	string memory symbol) 	 

 	ERC721(name, symbol) {

    }

    function safeMint(address to, string memory uri) public returns (uint) {

   	 _tokenIdCounter.increment();

   	 _safeMint(to, _tokenIdCounter.current());

   	 // base URI for NFT. Must end with /

   	 _uris\[_tokenIdCounter.current()\] = uri;

   	 return _tokenIdCounter.current();

    

    }

    

    function tokenURI(uint256 tokenId) public view override returns (string memory) {

    	return _uris\[tokenId\];

    }

}

This is a very simple token that inherited from OpenZeppelin’s ERC-721 implementation which you can see here: [https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC721/ERC721.sol](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC721/ERC721.sol)

![](https://qb-content-staging.s3.ap-south-1.amazonaws.com/public/fb231f7d-06af-4aff-bca3-fd51cb633f77/21c67865-35a6-49c3-915d-dfbf01251c8c.jpg)

We will be using OpenZeppelin, which is a framework for Solidity smart contract development. This framework allows us to reuse a fair amount of code that has already been written, deployed and tested by the OpenZeppelin community.

All tokens in Ethereum need to include a name (for example “MyFirstToken”) and a symbol (for example “MFT”). The symbol is shorter, usually up to 4 letters, and it is used to list the token in applications such as wallets, exchanges, and so on.

Making an analogy with physical coins, creating new tokens is called “minting”. As NFTs are tokens, creating an NFT is also called minting. Here there is a subtlety that you will probably want to understand. When you mint a new NFT, you specify an address to be the owner of the newly-minted NFT. That address can be a user-controlled address, or it can be a contract (because contracts control their own address, and can so hold Ether and tokens). If the address is a contract, that contract must implement the function onERC721Received, so we know that it is capable of handling an NFT, or else the NFT will be forever locked inside that contract. So we will use the safeMint function, which performs this check before actually minting it.

NFTs are usually used to claim ownership of some digital item, so they usually include a pointer to that digital item, in the form of a URI, or Uniform Resource Identifier. This is a sequence of characters defined by a standard, and typical examples are:

- https://google.com
- ipfs://bafybeidfjqmasnpu6z7gvn7l6wthdcyzxh5uystkky3xvutddbapchbopi/no-time-to-explain.jpeg

The first URI is a web link. The second URI is an IPFS link. The IPFS (InterPlanetary File System) is a very interesting and quite popular decentralized file system. This means a file system that does not have a central server but runs on an indefinite number of computers on the internet. The IPFS is usually the file system of choice in Web3 (decentralized) applications.

In the code, note the following:

1. the contract “inherits” (uses code) from OpenZeppelin’s ERC721 (NFT) implementation
2. there is a mapping to store the URI for each NFT
3. the constructor allows you to specify a name and a symbol for your NFTs
4. we include a safeMint function which allows you to specify a URI for each NFT that you mint
5. we include a tokenURI function which allows you to retrieve the URI for each NFT that you mint

Now open the compilation tab, select the 0.8.0 compiler to match the one in the code, and compile the file using the “Compile” button on the lower left.

![](https://qb-content-staging.s3.ap-south-1.amazonaws.com/public/fb231f7d-06af-4aff-bca3-fd51cb633f77/28a852a8-8638-4a9c-9874-c40e769bbd3a.jpg)

It should compile. If it does not, verify your code for typos.

Now open the deployment tab and select the following:

1. deploy on Javascript VM
2. use the first account from the list of accounts
3. compile MyNFT.sol (select it from the list of contracts)
4. You have to set a name and a symbol, so next to the “Deploy” button enter, for example: MyNFT, MNFT

Then click on the “Deploy” button.

 

![](https://qb-content-staging.s3.ap-south-1.amazonaws.com/public/fb231f7d-06af-4aff-bca3-fd51cb633f77/839eb504-b721-4dcb-8a34-cef0c5ee2d1b.jpg)

On the lower left, you will see your newly-deployed contract with all the required ERC-721 functions, some created from the code that you entered, and some created from the code in the OpenZeppelin implementation.

Click on the “>” symbol on the left of “MyNFT at 0x…” and you will see a button for each available function.

![](https://qb-content-staging.s3.ap-south-1.amazonaws.com/public/fb231f7d-06af-4aff-bca3-fd51cb633f77/e214fdb0-9cc8-4f77-b844-b1543a998a09.jpg)

__Subquest 3: Real-World Applications of NFTs__

These unique or non-fungible tokens solve a different kind of problem. They are used, for example, to:

- [represent proof of ownership of unique ](https://ethereum.org/en/nft/)physical[ items and their ](https://ethereum.org/en/nft/)properties, like scarcity, uniqueness[ - they let us tokenize things like art, collectables, even real estate](https://ethereum.org/en/nft/)

[https://opensea.io/assets/0x495f947276749ce646f68ac8c248420045cb7b5e/37198557236742699499983501232576879831168205667897545918004478909888772177921](https://opensea.io/assets/0x495f947276749ce646f68ac8c248420045cb7b5e/37198557236742699499983501232576879831168205667897545918004478909888772177921)

[https://opensea.io/assets/0x495f947276749ce646f68ac8c248420045cb7b5e/13632994468318124890034109068955230285460719526212263487938963180003346350081](https://opensea.io/assets/0x495f947276749ce646f68ac8c248420045cb7b5e/13632994468318124890034109068955230285460719526212263487938963180003346350081)

- represent an in-game item

[https://opensea.io/assets/0x548c407d35cdd3c812458d9ef6d135963f9f7ece/4959](https://opensea.io/assets/0x548c407d35cdd3c812458d9ef6d135963f9f7ece/4959)

[https://opensea.io/assets/0x548c407d35cdd3c812458d9ef6d135963f9f7ece/4839](https://opensea.io/assets/0x548c407d35cdd3c812458d9ef6d135963f9f7ece/4839)

[https://opensea.io/assets/0x548c407d35cdd3c812458d9ef6d135963f9f7ece/2100](https://opensea.io/assets/0x548c407d35cdd3c812458d9ef6d135963f9f7ece/2100)

- represent a ticket that gives you access to an event

[https://opensea.io/assets/0x2f7445cf648fd1d4d299e4bd0a550df697de055b/533](https://opensea.io/assets/0x2f7445cf648fd1d4d299e4bd0a550df697de055b/533)

[https://opensea.io/assets/0x35f7319878556806e9f5b66f9d3b4506c16d3bbb/1](https://opensea.io/assets/0x35f7319878556806e9f5b66f9d3b4506c16d3bbb/1)

[https://opensea.io/assets/0x35f7319878556806e9f5b66f9d3b4506c16d3bbb/118](https://opensea.io/assets/0x35f7319878556806e9f5b66f9d3b4506c16d3bbb/118)

- represent a domain name

[https://opensea.io/assets/0xd1e5b0ff1287aa9f9a268759062e4ab08b9dacbe/33558375478984928877993061732933007491654478165905677882145433970348574138940](https://opensea.io/assets/0xd1e5b0ff1287aa9f9a268759062e4ab08b9dacbe/33558375478984928877993061732933007491654478165905677882145433970348574138940)

[https://opensea.io/assets/0xd1e5b0ff1287aa9f9a268759062e4ab08b9dacbe/15844547572880000942399108386843197136558339689516786404618975729901406696165](https://opensea.io/assets/0xd1e5b0ff1287aa9f9a268759062e4ab08b9dacbe/15844547572880000942399108386843197136558339689516786404618975729901406696165)

- represent a unique piece of digital artwork (examples follow)

[https://opensea.io/assets/0x1db61fc42a843bad4d91a2d788789ea4055b8613/3773](https://opensea.io/assets/0x1db61fc42a843bad4d91a2d788789ea4055b8613/3773)

[https://opensea.io/assets/matic/0xa5f1ea7df861952863df2e8d1312f7305dabf215/88086](https://opensea.io/assets/matic/0xa5f1ea7df861952863df2e8d1312f7305dabf215/88086)

- represent a digital collectable (think of CryptoKitties)

[https://opensea.io/assets/0x099689220846644f87d1137665cded7bf3422747/8787](https://opensea.io/assets/0x099689220846644f87d1137665cded7bf3422747/8787)

[https://opensea.io/assets/0x495f947276749ce646f68ac8c248420045cb7b5e/73881852512585366829397768378841787039894851789237845675354749252870395133953](https://opensea.io/assets/0x495f947276749ce646f68ac8c248420045cb7b5e/73881852512585366829397768378841787039894851789237845675354749252870395133953)

__Subquest 4: Interact with your NFT using Remix.__

We are now going to use remix to simulate API calls to the main functions of our recently created NFT token. If you do not see your deployed contract (probably because you closed the browser at some point) just go back, compile and deploy again.

__Name__

![](https://qb-content-staging.s3.ap-south-1.amazonaws.com/public/fb231f7d-06af-4aff-bca3-fd51cb633f77/3c263538-c6a0-48c1-9660-dd3e80fe8aab.jpg)

Click on the “name” button, and you will see a line appearing on the console. Click on the symbol on the right of that line, and you will be able to see the details of this call. Notice the following: { "0": "string: MyNFT" }

__Mint__

![](https://qb-content-staging.s3.ap-south-1.amazonaws.com/public/fb231f7d-06af-4aff-bca3-fd51cb633f77/786d27a0-96fe-463a-bfc2-c4d80049a85b.jpg)

Next to the “safeMint” button, enter your address from MetaMask, and a URI that will be linked to the newly created NFT. This means that this URI will be stored alongside the NFT inside the contract, and so that URI will be forever a companion of this NFT.

For example, you would enter:

-  0x5B38Da6a701c568545dCfcB03FcB875f56beddC4 (but do not use this address, use the address displayed next to “ACCOUNT”  in your Remix, as shown on the figure)
- ipfs://QmbYptqPMSaYR6qUoMqovhfQwWS29MBTmGJSL41QQ4qanf

![](https://qb-content-staging.s3.ap-south-1.amazonaws.com/public/fb231f7d-06af-4aff-bca3-fd51cb633f77/f70f92de-85b9-4714-bc46-2798377a577c.jpg)

Now click on the “safeMint” button, and you will see a line appearing on the console. Click on that line, and you will be able to see the details of this call.

Notice the following:

{ "address to": "0x5B38Da6a701c568545dCfcB03FcB875f56beddC4",

	"string uri": "QmbYptqPMSaYR6qUoMqovhfQwWS29MBTmGJSL41QQ4qanf" }

__Get the Token URI__

![](https://qb-content-staging.s3.ap-south-1.amazonaws.com/public/fb231f7d-06af-4aff-bca3-fd51cb633f77/2eaf589b-c0f5-4c97-bb62-640ff3d92436.jpg)

Next to tokenURI, enter the ID for the token recently created, in our example, 1. Look at the output on the right. Notice the following:

{ "0": "string: QmbYptqPMSaYR6qUoMqovhfQwWS29MBTmGJSL41QQ4qanf" }

Here you are getting the IPFS CID that we entered as URI in the previous step.

__Get the Token Owner__

![](https://qb-content-staging.s3.ap-south-1.amazonaws.com/public/fb231f7d-06af-4aff-bca3-fd51cb633f77/665bc97c-3039-4049-9a5c-e77464c00cbb.jpg)

Next to ownerOf, enter the ID for the token recently created, in our example, 1. Look at the output on the right. Notice the following:

{ "0": "address: 0x5B38Da6a701c568545dCfcB03FcB875f56beddC4" }

Here you are getting the address of the NFT’s owner. You may remember, from subquests 2 and 4 that, when minting (creating) an NFT, we passed an address as a parameter. That address will “own” the token, and so it will be the only one that can transfer it to another address.

__Transfer__



Now next to transferFrom, enter the following:

1. the address that owns the token (the first in your list of addresses):

0x5B38Da6a701c568545dCfcB03FcB875f56beddC4

1. a new address to transfer the NFT to (for example, the second in your list of addresses):

0xAb8483F64d9C6d1EcF9b849Ae677dD3315835cb2

1. the token ID (in our example, 1)

Then click the button.

Notice the following in the console:

{ "address from": "0x5B38Da6a701c568545dCfcB03FcB875f56beddC4", "address to": "0xAb8483F64d9C6d1EcF9b849Ae677dD3315835cb2", "uint256 tokenId": { "_hex": "0x01", "_isBigNumber": true } }

The NFT is now owned by the second address.

Click again the “ownerOf” button. Notice the following output:

{ "0": "address: 0xAb8483F64d9C6d1EcF9b849Ae677dD3315835cb2" }

__Subquest 5: Deploy your token to a public test network__

Use a Testnet Faucet to get some toy ether.

1. open MetaMask and select the Ropsten test network
2. copy your Ethereum address
3. go to [https://faucet.ropsten.be/](https://faucet.ropsten.be/)
4. paste your address

![](https://qb-content-staging.s3.ap-south-1.amazonaws.com/public/fb231f7d-06af-4aff-bca3-fd51cb633f77/f4513842-911c-4dd8-9bb7-ce052c498f51.jpg)

1. Click on the button
2. Wait until your receive your test Ether, this usually happens in a few minutes

Now that we have some balance, we are going to deploy our NFT collection to the Ropsten test network.

If you are not logged in to MetaMask, log in now.

![](https://qb-content-staging.s3.ap-south-1.amazonaws.com/public/fb231f7d-06af-4aff-bca3-fd51cb633f77/a967bf7f-b355-4ec1-8e5b-0da9643abe79.jpg)

Go to Remix and select the “Injected Web3” environment.

Select the MyNFT contract.

Next to the “Deploy” button enter a name and a symbol for our token.

Click on Deploy.

When the MetaMask window opens, click on “Confirm”.

Now wait for the token to be deployed, this usually happens in a couple of minutes.

Once it deploys, you will see a MetaMask notification in the upper right.

![](https://qb-content-staging.s3.ap-south-1.amazonaws.com/public/fb231f7d-06af-4aff-bca3-fd51cb633f77/797c1ee1-7611-4b3c-b447-c8c13d1a364e.jpg)

__Subquest 6: Interact with your NFT using a wallet__

We will use MetaMask mobile to interact with your NFT.

1. install the MetaMask mobile wallet in your phone
2. select the Ropsten network
3. if you have more than one address, select the same address that you used in the previous subquest
4. add your recently deployed contract as a custom token, using:
	1. the address from here:

![](https://qb-content-staging.s3.ap-south-1.amazonaws.com/public/fb231f7d-06af-4aff-bca3-fd51cb633f77/888dd3cf-5e77-4243-8f6c-064978beb59f.jpg)

- 
	1. the symbol, in our example “MNFT”
	2. zero as decimals

![](https://qb-content-staging.s3.ap-south-1.amazonaws.com/public/fb231f7d-06af-4aff-bca3-fd51cb633f77/985f7cc9-5359-45ed-b397-476f7f4499e9.jpg)

Now follow the steps in subquest 4, subtitle “Mint”, to mint a new NFT in the testnet deployed contract. The only difference will be that a MetaMask window will appear, click on “Confirm” as before.

Wait for your transaction to be processed.

Check your NFT

![](https://qb-content-staging.s3.ap-south-1.amazonaws.com/public/fb231f7d-06af-4aff-bca3-fd51cb633f77/e4bbaa15-5f98-4f64-89ae-d0663ba27a3b.jpg)

Congratulations! You have created your first NFT.

Now that you know how to do it, if you want to practice a little more, I recommend the following:

1. install IPFS desktop client
2. upload a few pictures to it
3. copy the CIDs from the IPFS desktop client, and prefix them with “ipfs://” to get the IPFS links
4. create a few more NFTs using those links