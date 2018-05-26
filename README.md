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
