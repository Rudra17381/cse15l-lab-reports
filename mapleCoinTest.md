# Maple coin, [original site link](https://maple-coin.com)
---

Note: The entire original site is designed by me and I am the sole owner of it which is why I am using its content here and replicating its homepage to create this markdown file.

---
Maple Coin is an innovative perspective on currency. It is a fully digital currency developed entirely from scratch by a high school student. It is a cryptocurrency that relies on blockchain technology based on decentralized consensus, making it safer than every physical currency currently in existence. This revolutionary technology is the future of currencies; Be a fundamental part of this future by participating in the Maple Coin Network today

## What is a cryptocurrency? Why use it?
---
*Cryptocurrency is a digital currency that is not controlled by any single entity such as a government or a bank*. It roams free of every border and is built upon and maintained by **clever mathematical ideas** and **algorithms**, making it practically impossible and theoretically implausible to break. It is free of the risk of any corruption, which is a possibility in currencies governed by a single body like a government and is instead controlled by the people using it, making it the most secure form of currency.

A cryptocurrency gives its users the peace of mind of their money being safe as there is no being behind it; it's all just mathematics! It also provides an easy outlet for people to invest in and contribute to the growth of this revolutionary technology. Cryptocurrencies are the people's currencies, and hence they have a bright future ahead of them where they might soon be replacing physical currencies forever and for good.

Maple Coin is a breath of fresh air in the world of cryptocurrencies. It is committed to using its robust infrastructure to facilitate and promote the safe and secure exchange of money between individuals and entities. It is a contribution to the growth of cryptocurrencies and will get just better with time.

## Inspiration
---
This project is heavily inspired by `Blockchain at Berkeley` and the YouTube channel `3Blue1Brown`.

The following lecture materials and video are the sole sources of the foundation of this project:

1. [Bitcoin Mechanics and Optimizations: A Technical Overview - Blockchain at Berkeley](https://blockchain.berkeley.edu/courses/spring-2020-fundamentals-decal/)
2. [Bitcoin IRL: Wallets, Mining, and More - Blockchain at Berkeley](https://blockchain.berkeley.edu/courses/spring-2020-fundamentals-decal/)
3. [Trust without Trust: Distributed Systems & Consensus - Blockchain at Berkeley](https://blockchain.berkeley.edu/courses/spring-2020-fundamentals-decal/)
4. [But how does bitcoin actually work? - 3Blue1Brown](https://www.youtube.com/watch?v=bBC-nXj3Ng4&feature=youtu.be)

## Code
---

> * Open Source Maple Coin Mining Software: [Mining Software](http://maple-coin.com/mining)
> * Open Source Maple Coin Network Code: [Source Code](http://maple-coin.com/sourceCode)

## Example Mining Code
---
```
class Miner(Network):
    """
    This class constructs the Miner object, where all the mining related stuff resides
    This object gets all the required data, constructs blocks and then mines for the nonce of said block
    It returns said block once mined
    """

    def __init__(self):
        """
        Initializing all the required data for Mining; Note that it does not have any dependencies on arguments and dereives
        the needed data solely from the Network class's static methods, due to this the object is pickle safe and can be used 
        in multiprocessing and multithreading more easily without needing any janky workarounds
        """

        #Getting Pending Transactions and all the needed info for the new block and parsing it
        self.pendingTransactions = Network.newTransactions()
        newBlockInfo = Network.newBlockInfo()
        self.previousBlockHash = newBlockInfo["previousBlockHash"]
        self.newBlockIndex = newBlockInfo["id"]
        self.hashPuzzle = newBlockInfo["hashPuzzle"]
        self.maxTransactions = newBlockInfo["maxTransactions"]

        #Verfiying the transactions to be placed into the block and adhereing to the block limit
        self.transactions = self.getValidTransactions()[0:self.maxTransactions]
        #Future block attribute
        self.block = None

    def getValidTransactions(self):
        """
        This instance method gets all the valid transactions from the pending transactions
        To validate a transaction it verifies it's signature
        """

        #To store valid transactions
        transactions = []

        for transaction in self.pendingTransactions:

            #Trying to verify because rsa verify throws error when signature is fradulent
            try:   
                
                #Verify transaction and add it to the valid transactions list
                if rsa.verify(transaction.stringTransactions().encode('utf8'), transaction.signature, rsa.PublicKey(int(transaction.publicKey), int(transaction.exponent))):
                    transactions.append(transaction)
            except:
                continue
        
        #Return the valid transactions
        return transactions

    def calculateHash(self):
        """
        This instance method calulates the hash of the given block
        """

        #Forms the string represtation of the block according to Maple Coin Standard Specfications
        self.block.time = datetime.datetime.now().strftime("%Y-%m-%d %H:%M")
        stringBlock = (
            str(self.block.time) + 
            self.block.merkelRoot + 
            (self.block.previousBlockHash if self.block.previousBlockHash != "None" else "") + 
            str(self.block.newBlockIndex) + 
            str(self.block.nonce)
        )

        #Hashes the string block and returns it
        return hashlib.sha3_512(stringBlock.encode('utf8')).hexdigest()

    def mine(self):
        """
        This instance method is the mining algorithm for Maple Coin Blocks 
        It starts at a random nonce, and keeps incrementing from there
        Calculates hash for each said nonce, if hash meets the hash puzzle, it stops, else repeats
        Every said minutes, it checks if a block has already been discovered, if so it stops, else continues
        """

        #setting time to check for block discovery
        startTime, check= datetime.datetime.now(), False

        #setting initial block nonce and hash
        self.block.nonce = random.randint(*nonceStartBounds)
        self.block.hash = self.calculateHash()
        
        #while the hash puzzle is not solved
        while self.block.hash[0:len(self.hashPuzzle)] != self.hashPuzzle:

            #checking for block discovery once every said minutes
            if ((datetime.datetime.now().minute - startTime.minute) % Network.minuteCheck) == 0:    
                if not check:
                    if self.currentBlockSearchIndex() > int(self.block.newBlockIndex):
                        break
                check = True
            else:
                check = False

            #increment nonce and caculate new hash
            self.block.nonce += 1
            self.block.hash = self.calculateHash()

    def mineBlock(self):
        """
        This instance method constructs a block from precompiled data and then mines for it's nonce
        """

        #Construct block and mine nonce
        self.block = Block(self.transactions, self.newBlockIndex, self.previousBlockHash)
        self.mine()
```

## An image of Gisel library cus why not
---
![Image](https://ucsdnews.ucsd.edu/news_uploads/Resized_Geisel_Library_08.31.jpg)
