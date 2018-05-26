How to implement Blockchain
======
- Author: Wenzhuo Liang
- Email: wzliangtech@gmail.com
- Wechat: wzliang1988

## Blockchain
What is blockchain? A blockchain is a distributed database that is used to store continuously growing list of records.
How to implement this system? Let's answer the following critical questions.

### How to save records
- Record is continuously growing, how do we deal with it?
- How to modify previous records?

Solution
- Just like logging, continously add new log, then concast them
- Actually this is LinkedList

```Java
Class DataBlock(){
    getData();
    setData();
    getPre();
    getNext();
}
```
Can the record be modified? If the record can be modified, that will cause synchronized problem. So can we make the record unmodified? Actually, the architecture of GFS is built on top of an unmodified data structure.</br>
So, we need to build unmodified list of records.</br>
Even though record cannot be modified, data view can be modified.</br>
How to make people confident in the record and trust that it is true. Everyone has the same record.</br>

### How to add a new record
Every new record is added, we will need to use the same method to add it into everyone's copy.</br>
Can we have the compute power? And why? We will need to make the data model generic</br>
How do we define the compute power? To answer this question, we will need to understand how to construct the distributed computer.</br>
Who generates the storage space? What do we save in every address? How does the record map to the address? We can store the logic of this record into this address. So what do we need to put in the address? Address information, data, code?</br>
Status is the collection of address and its mapped status. We will update the status through new transactions

### How to deal with the chaos
Who solves the problem first, who insert first</br>
Choose the longest linkedlist

## Nativecoin in Action
This example is to implement a Blockchain who supports Token</br>

### How to save record
Blockchain's concept - a distributed database that maintains a continuously growing list of ordered records. So it should have the following functionalities:

- A defined block and blockchain structure
- Methods to add new blocks to the blockchain with arbitrary data
- Blockchain nodes that communicate and sync the blockchain with other nodes
- A simple HTTP API to control the node

### Block structure
We will start by defining the block structure. Only the most essential properties are included at the block at this point.
- **index**: The height of the block in the blockchain 
- **data**: Any data that is included in the block
- **timestamp**: A timestamp
- **hash**: A sha256 hash token from the content of the block
- **previousHash**: A reference to the hash of the previous block. The value explicitly defines the previous block.

![data structure](i/blockchain.png)

The code for the block structure looks like:
```Typescript
class Block{

    public index: number;
    public hash: string;
    public previousHash: string;
    public timestamp: number;
    public data: string;
    
    constructor(index: number, hash: string, previousHash: string, timestamp: number, data: string) {
        this.index = index;
        this.previousHash = previousHash;
        this.timestamp = timestamp;
        this.data = data;
        this.hash = hash;
    }
}
```

### How to make sure the data is unmodified - Block Hash
The block has is one of most important properties of the block. The hash is calculated over all data of the block. This means that if anything in the block changes, the original hash is no longer valid. The block hash can also be thought as the unique identifier of the block. For instance, blocks with same index can appear, but they all have unique hashes.

We calculate the hash of the block using the following codes:
```Typescript
const calculateHash = (index: number, previousHash: string, timestamp: number, data: string): string =>
    CryptoJS.SHA256(index + previousHash + timestamp + data).toString();
```
We use the block hashes to preserve integrity of the block and to explictly reference the previous block.

An important consequence of the properties hash and previousHash is that a block can't be modified without changing the hash of every consecutive block.

