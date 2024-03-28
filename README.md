## Annonymous Voting with ZKP

This project tries to carry out annonymous voting using ZKPs. The premise is that a user can only vote once and will be private. We strive to demonstrate the capabilities of implementing zkp to perform annonymous voting (and checking if a user has voted only once) that can be implemented on any web app. 

A user first generates two random keys, one is public and one is secret. Then they can connect to a UI that requires voting via a wallet like Metamask and sign a signature to obtain a registration ticket (essentially a commitment). This registration ticket gets stored in the backend database and store on the public merkle tree on a smart contract (it takes the id and commitment of the user). 

Once validation is successful, the user can submit a vote. Now they are ready to submit their vote to the chain and it is verified by the merkle tree on the chain. The browser received the event that the commitment is submitted to the chain and generates the merkle tree and calculates the zk proof with its nullifier. This checks if the voter has voted before or not. Finally, their vote is officially submitted and logged on chain. 

![alt text](https://github.com/[username]/[reponame]/blob/[branch]/image.jpg?raw=true)
