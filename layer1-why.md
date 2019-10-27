---
title: Why Build A Layer1 Blockchain?
---

Nervos is a layered network, which is comprised of layers of protocols, rather than only one layer and one protocol as some other blockchains are.

## Why Is Layer1?

Before talking about Nervos's specific layers, let's first define what is a layered architecture and what is a layer1 blockchain.

The key difference between layer1 and layer2 is the consensus scope. Consensus scope means how many people will join the consensus process. Layer1 should have the broadest consensus, which is the global consensus. This is what permission-less blockchains are doing. Layer2 will have a smaller consensus scope, think Plasma. One Plasma usually only have 20–30 nodes. State Channel is also a layer2, you only need to reach consensus between two people.

## Why Layer2 has Smaller Consensus Scope?

Consensus is expensive.

To reach global consensus, the cost is very high. If we can reduce consensus scope, we will get a great performance and cost improvement. That's why a layered network has a potential to bring much more scalability.

Having layers is not only a scalability method, it's also a separation of concerns, which means different layers is responsible for different problems. This is useful for lots of problems we face today in blockchain world. 

For example, we can have computation on one layer and verification on another. We don't need to mix the two tasks together. The separation of computation and verification is very natural in other cryptography area. Like signature verification, someone generate the signature first, then someone else do the verification. Or like ZkSnark, someone generate the proof, someone else verify it. Layering is a very natural match to such separation.

We can also do separation to have a transaction layer and a value preservation layer, which is sometimes called store of value layer.

We can have compliance on one layer and neutrality on another. Many companies need to be compliant to financial regulations. We want to move real world assets to blockchain, but this is only doable on permission blockchain, cause we need KYC and AML. But how can you do it on a permission-less blockchain. Should layer1 protocol also comply to those regulations, or should it be neutral? We believe the layer1 blockchain should be neutral just like the Internet. It's hard to be compliant to all regulations, since there are so many countries on earth, and each of them has different regulations. But still we can do compliance on layer2, because it has much small consensus scope.

## Can any Blockchain Be Layer1?

With the definition clear, can any blockchain be layer1? Of course NOT.

For layer1, we want two things most. One is decentralization , that is for censorship-resistance, and the other is security, layer1 must be the most secure layer in the whole network. Because it is the foundation of security for the whole network.
Two most known blockchain project is Bitcoin and Ethereum, they both have global consensus and very secure. There are others out there, but in our definition, they are not layer1 blockchains. Because it has smaller consensus scope if you think carefully, say some chain has only 21 consensus node.

Why we build our own layer1 blockchain named CKB? Both Bitcoin and Ethereum were not designed for the scenarios we have in mind. Bitcoin is nearly perfect, but it is only for money, really limited scripting ability makes its hard to have broader use cases. Ethereum has a whole lot features, but still it was not designed as a layer1 protocol, which makes it hard to use it working with layer2 protocols.

That's why we designed CKB, its a layer1 blockchain with layer2 in mind.

## Conclusion

We see a world where economy runs on a stack of protocols. So we designed Nervos with that mindset, and have a layered solution. Layer1 protocol works well with layer2 ones and a neat separation of concerns makes the system both secure and scalable.

ref:

- https://www.youtube.com/watch?v=F1nfrTsGJqk
