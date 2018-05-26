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
