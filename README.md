0x4c9135af735b894d

# [Chapter1](https://github.com/emerald-dao/beginner-cadence-course/tree/main/chapter1.0)

## Day1

#### 1. Explain what the Blockchain is in your own words.

ブロックチェーンは、公共の場所に存在する石碑のようなもの。
暗号学的な鍵でアイデンティティを示すことで、誰でも情報を書き込んだり、読むことができる。
基本的な機能として、誰にいくらを送金するという意思を書き込むことで、送金システムが実現されている。
また、そこにはコンピュータプログラムも記録することができる。

A blockchain is like a stele that exists in a public place.
Anyone can write or read the information by indicating their identity with a cryptographic key.
The basic function of a money transfer system is to write the intention to send money to whom and how much.
Computer programs can also be recorded there.

#### 2. Explain what a Smart Contract is.

スマートコントラクトは、ブロックチェーン上に記録されたコンピュータプログラムである。
そこに書かれたルールに従って、多様なデジタル資産や創造物を構築できる。

A smart contract is a computer program recorded on a blockchain.
According to the rules written there, a wide variety of digital assets and creations can be constructed.

#### 3. Explain the difference between a script and a transaction.

スクリプトは、ブロックチェーンの情報を読み取るためのコード。無料で実行できる。
トランザクションは、ブロックチェーンの情報を書き換えてインタラクションするためのコード。こちらは手数料がかかる。

Script is code for reading blockchain information. It can be executed for free.
Transaction is the code to rewrite the blockchain information and interact with the blockchain. There is a fee for this.


## Day2

#### 1. What are the 5 Cadence Programming Language Pillars?

- Safety and Security
- Clarity
- Approachability
- Developer Experience
- Resource Oriented Programming

#### 2. In your opinion, even without knowing anything about the Blockchain or coding, why could the 5 Pillars be useful (you don't have to answer this for #5)?

All of these synergies will make the code simpler, safer and more secure. In particular, we can expect the following

- Safety and Security
  - Since a certain level of high safety and security is guaranteed at the time of compilation, it is easy to create vulnerability-free code even if you are not a security expert.

- Clarity
  - It can make the code simpler and reduce the occurrence of bugs.

- Approachability
  - This is useful for increasing the quality of code and for increasing the number of developers.

- Developer Experience
  - Developer experience plays a major role in creating code that is maintainable and sustainable over time.


# [Chapter2](https://github.com/emerald-dao/beginner-cadence-course/tree/main/chapter2.0)

## Day1

#### 1. Deploy a contract to account `0x03` called "JacobTucker". Inside that contract, declare a **constant** variable named `is`, and make it have type `String`. Initialize it to "the best" when your contract gets deployed.

https://play.onflow.org/70008c75-5567-4b28-84b8-1298ac6fb6a1?type=account&id=e95c5ef8-066d-4797-94a3-dfe6f0562449&storage=none

```cadence
pub contract JacobTucker {
    pub let is: String

    init() {
        self.is = "the best"
    }
}
```

#### 2. Check that your variable `is` actually equals "the best" by executing a script to read that variable. Include a screenshot of the output.
<img width="1124" alt="ScreenShot 2022-05-03 16 46 18" src="https://user-images.githubusercontent.com/10495516/166419921-8b27819d-26cb-41cb-a3da-b489d1d0c7f0.png">

## Day2

#### 1. Explain why we wouldn't call `changeGreeting` in a script.

Because that function performs an operation that changes the state of the blockchain, it must use a transaction rather than a read-only script.

#### 2. What does the `AuthAccount` mean in the `prepare` phase of the transaction?

`AuthAccount` is an object to access the account's storage of the authorizer of a transaction. Using its methods, it is possible to store/load resource objects and create/remove links to the account's storage.

#### 3. What is the difference between the `prepare` phase and the `execute` phase in the transaction?

The prepare phase is where you can access storage for the transaction authorizer's account. Here, resource objects needed for operations are loaded from storage and stored in transaction variables.

The execution phase uses the transaction's variables to call functions on the objects loaded in the prepare phase.

Proper use of these phases increases the readability of the transaction code and facilitates static analysis.

#### 4. Add `updateMyNumber` feature

https://play.onflow.org/213bee4c-9fcf-4bf7-873e-dcbb623be6c5?type=account&id=bfdfeb42-6f20-4329-8148-0e5fb8648626&storage=none


## Day3

#### 1. In a script, initialize an array (that has length == 3) of your favourite people, represented as `String`s, and `log` it.

```cadence
pub fun main() {
  let favoritePeople: [String] = [
    "Kumagusu Minakata",
    "Aristotle",
    "Alexander von Humboldt"
  ]
  log(favoritePeople)
}
```

#### 2. In a script, initialize a dictionary that maps the `String`s Facebook, Instagram, Twitter, YouTube, Reddit, and LinkedIn to a `UInt64` that represents the order in which you use them from most to least. For example, YouTube --> 1, Reddit --> 2, etc. If you've never used one before, map it to 0!

```cadence
pub fun main() {
  let servicePriorities: {String: UInt64} = {
    "Facebook": 6,
    "Instagram": 3,
    "Twitter": 1,
    "YouTube": 2,
    "Reddit": 4,
    "LinkedIn": 5
  }
  log(servicePriorities)
}
```

#### 3. Explain what the force unwrap operator `!` does, with an example different from the one I showed you (you can just change the type).

For example, the force unwrap operator is used to cast generic types in Cadence.

```cadence
pub struct interface BaseStruct {
}

pub struct Struct1: BaseStruct {
  pub fun hello1() {
    log("hello struct 1")
  }
}

pub struct Struct2: BaseStruct {
  pub fun hello2() {
    log("hello struct 2")
  }
}

pub fun main() {
  let aStruct: AnyStruct{BaseStruct} = Struct1()
  (aStruct as! Struct1).hello1()
}
```

#### 4. Using this picture below, explain...

- What the error message means
  - The return type of the script is expected to be a `String`, but the current code returns a `String?` type (an `Optional` type of `String`), which is not the correct type.

- Why we're getting this error
  - If a key is specified with a `Dictionary` type, the return value is an `Optional` type. This is because there may be no value at the specified key location.

- How to fix it
  - Change the return type to `String?` or change the part where the value is taken from the dictionary to `thing[0x03]!` (To make it safer, use `thing[0x03] ?? ""` is preferred).


## Day4

#### 1. Deploy a new contract that has a Struct of your choosing inside of it (must be different than `Profile`).

https://play.onflow.org/2b83a919-539d-4bec-82af-14e2ef396c2a?type=account&id=76999673-060d-4faa-99dc-7b1720c99be0&storage=none

```cadence
pub contract StorageV1 {
    pub struct File {
        pub let path: String
        pub let data: String

        init(path: String, data: String) {
            self.path = path
            self.data = data
        }
    }
}
```

#### 2. Create a dictionary or array that contains the Struct you defined.

https://play.onflow.org/2b83a919-539d-4bec-82af-14e2ef396c2a?type=account&id=00e3d74a-b1c4-4805-8f03-99ee3606ca6b&storage=none

```cadence
pub contract StorageV2 {
    pub var files: {String: File}

    pub struct File {
        pub let path: String
        pub let data: String

        init(path: String, data: String) {
            self.path = path
            self.data = data
        }
    }

    init() {
        self.files = {}
    }
}
```

#### 3. Create a function to add to that array/dictionary.

https://play.onflow.org/2b83a919-539d-4bec-82af-14e2ef396c2a?type=account&id=7eb06053-67da-43a2-b12f-18aa06a5601b&storage=none

```cadence
pub contract StorageV3 {
    pub var files: {String: File}

    pub struct File {
        pub let path: String
        pub let data: String

        init(path: String, data: String) {
            self.path = path
            self.data = data
        }
    }

    pub fun addFile(path: String, data: String) {
        let newFile = File(path: path, data: data)
        self.files[path] = newFile
    }

    pub fun getFile(path: String): File? {
        return self.files[path]
    }

    init() {
        self.files = {}
    }
}
```

#### 4. Add a transaction to call that function in step 3.

https://play.onflow.org/2b83a919-539d-4bec-82af-14e2ef396c2a?type=tx&id=2762d023-75c5-45c3-b288-1e1e8d27afa4&storage=none

```cadence
import StorageV3 from 0x03

transaction {
  prepare(acct: AuthAccount) {
    StorageV3.addFile(path: "/testFile.dat", data: "test")
  }
}
```

#### 5. Add a script to read the Struct you defined.

https://play.onflow.org/2b83a919-539d-4bec-82af-14e2ef396c2a?type=script&id=ddb19ec0-cb22-4e7b-bcdb-7ba2317c69ed&storage=none

```cadence
import StorageV3 from 0x03

pub fun main(): StorageV3.File? {
  return StorageV3.getFile(path: "/testFile.dat")
}
```


# [Chapter3](https://github.com/emerald-dao/beginner-cadence-course/tree/main/chapter3.0)

## Day1

#### 1. In words, list 3 reasons why structs are different from resources.

1. Structs can be copied
2. Structs can be lost (or overwritten)
3. Structs can be created at anytime, anywhere

#### 2. Describe a situation where a resource might be better to use than a struct.

Resources are ideal if you want to handle valuable NFTs and other items that you don't want accidentally copied or lost in the digital world.

#### 3. What is the keyword to make a new resource?

`create`

#### 4. Can a resource be created in a script or transaction (assuming there isn't a public function to create one)?

No, it is impossible.

#### 5. What is the type of the resource below?

A resource type called `Jacob`

```cadence
pub resource Jacob {

}
```

#### 6. Let's play the "I Spy" game from when we were kids. I Spy 4 things wrong with this code. Please fix them.

```cadence
pub contract Test {

    // Hint: There's nothing wrong here ;)
    pub resource Jacob {
        pub let rocks: Bool
        init() {
            self.rocks = true
        }
    }

    pub fun createJacob(): Jacob { // there is 1 here
        let myJacob = Jacob() // there are 2 here
        return myJacob // there is 1 here
    }
}
```

↓

```cadence
pub contract Test {
    pub resource Jacob {
        pub let rocks: Bool
        init() {
            self.rocks = true
        }
    }

    pub fun createJacob(): @Jacob {
        let myJacob <- create Jacob()
        return <- myJacob
    }
}
```

## Day2

#### 1. Write your own smart contract that contains two state variables: an array of resources, and a dictionary of resources. Add functions to remove and add to each of them. They must be different from the examples above.

```cadence
pub contract ResourceHolder {
    pub let resourceArray: @[SampleResource]
    pub let resourceDictionary: @{String: SampleResource}

    pub resource SampleResource {
        pub let name: String

        init(name: String) {
            self.name = name
        }
    }

    pub fun addToArray(name: String) {
        self.resourceArray.append(<- create SampleResource(name: name))
    }

    pub fun removeFromArray(index: Int) {
        let sampleResource <- self.resourceArray.remove(at: index)
        destroy sampleResource
    }

    pub fun addToDictionary(name: String) {
        self.resourceDictionary[name] <-! create SampleResource(name: name)
    }

    pub fun removeFromDictionary(name: String) {
        let sampleResource <-  self.resourceDictionary.remove(key: name) ?? panic("Not Found")
        destroy sampleResource
    }

    init() {
        self.resourceArray <- []
        self.resourceDictionary <- {}
    }
}
```

## Day3

#### 1. Define your own contract that stores a dictionary of resources. Add a function to get a reference to one of the resources in the dictionary.

```cadence
pub contract ResourceHolder {
    pub let resources: @{String: SampleResource}

    pub resource SampleResource {
        pub let name: String

        init(name: String) {
            self.name = name
        }
    }

    pub fun add(name: String) {
        self.resources[name] <-! create SampleResource(name: name)
    }

    pub fun remove(name: String) {
        let sampleResource <-  self.resources.remove(key: name) ?? panic("Not Found")
        destroy sampleResource
    }

    pub fun borrow(name: String): &SampleResource {
        return &self.resources[name] as! &SampleResource
    }

    init() {
        self.resources <- {}
        self.add(name: "test1")
    }
}
```

#### 2. Create a script that reads information from that resource using the reference from the function you defined in part 1.

```cadence
import ResourceHolder from 0x01

pub fun main(): String {
  let ref = ResourceHolder.borrow(name: "test1")
  return ref.name
}
```

#### 3. Explain, in your own words, why references can be useful in Cadence.

Because you can call that function without moving the resource itself. This is essential in order to have someone other than yourself call some of the functions of a resource that you have.


## Day4

#### 1. Explain, in your own words, the 2 things resource interfaces can be used for (we went over both in today's content)

1. To allow resources/structures with common necessary functions to be generalized and handled together.

2. Use it to expose only some functions of your resources to others.

#### 2. Define your own contract. Make your own resource interface and a resource that implements the interface. Create 2 functions. In the 1st function, show an example of not restricting the type of the resource and accessing its content. In the 2nd function, show an example of restricting the type of the resource and NOT being able to access its content.

```cadence
pub contract ResourceHolder {
    access(contract) var memo: @Memo

    pub resource interface MemoPublic {
        pub fun read(): String
    }

    pub resource Memo: MemoPublic {
        pub let name: String
        access(self) var content: String

        pub fun read(): String {
            return self.content
        }

        pub fun rewrite(content: String) {
            self.content = content
        }

        init(name: String, content: String) {
            self.name = name
            self.content = content
        }
    }

    pub fun rewriteMemo(content: String) {
        let ref = &self.memo as! &Memo
        ref.rewrite(content: content)
    }

    pub fun readMemo(): String {
         let ref = &self.memo as! &AnyResource{MemoPublic}
         return ref.read()
    }

    init() {
        self.memo <- create Memo(name: "test name", content: "test content")
    }
}
```

#### 3. How would we fix this code?

```cadence
pub contract Stuff {

    pub struct interface ITest {
      pub var greeting: String
      pub var favouriteFruit: String
    }

    // ERROR:
    // `structure Stuff.Test does not conform 
    // to structure interface Stuff.ITest`
    pub struct Test: ITest {
      pub var greeting: String

      pub fun changeGreeting(newGreeting: String): String {
        self.greeting = newGreeting
        return self.greeting // returns the new greeting
      }

      init() {
        self.greeting = "Hello!"
      }
    }

    pub fun fixThis() {
      let test: Test{ITest} = Test()
      let newGreeting = test.changeGreeting(newGreeting: "Bonjour!") // ERROR HERE: `member of restricted type is not accessible: changeGreeting`
      log(newGreeting)
    }
}
```

↓

```cadence
pub contract Stuff {

    pub struct interface ITest {
      pub var greeting: String
      pub var favouriteFruit: String
      pub fun changeGreeting(newGreeting: String): String // **Added**
      pub fun changeFavouriteFruit(favouriteFruit: String): String // **Added** MEMO: Not essential, but I'd like to include this one.
    }

    pub struct Test: ITest {
      pub var greeting: String
      pub var favouriteFruit: String // **Added**

      pub fun changeGreeting(newGreeting: String): String {
        self.greeting = newGreeting
        return self.greeting // returns the new greeting
      }

      // **Added** MEMO: Not essential, but I'd like to define this one.
      pub fun changeFavouriteFruit(favouriteFruit: String): String {
        self.favouriteFruit = favouriteFruit
        return self.favouriteFruit // returns the new favouriteFruit
      }

      init() {
        self.greeting = "Hello!"
        self.favouriteFruit = "Apple" // **Added**
      }
    }

    pub fun fixThis() {
      let test: Test{ITest} = Test()
      let newGreeting = test.changeGreeting(newGreeting: "Bonjour!")
      log(newGreeting)
    }
}
```

## Day5

#### In each AREA (1, 2, 3, and 4), I want you to do the following: for each variable (a, b, c, and d), tell me in which areas they can be read (read scope) and which areas they can be modified (write scope). For each function (publicFunc, contractFunc, and privateFunc), simply tell me where they can be called.

- read scope
  - a: AREA 1, 2, 3 and 4
  - b: AREA 1, 2, 3 and 4
  - c: AREA 1, 2 and 3
  - d: AREA 1

- write scope
  - a: AREA 1, 2, 3 and 4
  - b: AREA 1
  - c: AREA 1
  - d: AREA 1

- publicFunc: AREA 1, 2, 3 and 4
- contractFunc: AREA 1, 2 and 3
- privateFunc: AREA 1


# [Chapter4](https://github.com/emerald-dao/beginner-cadence-course/tree/main/chapter4.0)

## Day1

#### 1. Explain what lives inside of an account.

Within an account, there is a contract code area and an account storage area. The contract code area contains the code of the contracts deployed by the account. Account Storage can be stored objects such as resources and the link for them.

#### 2. What is the difference between the `/storage/`, `/public/`, and `/private/` paths?

The `/storage/` path can be stored the object itself, such as a resource.

The `/public/` paths can be stored links to resource objects stored in the storage path, which can be accessed by anyone.

The `/private/` path can also be stored links to resource objects, but these cannot be accessed by anyone.

#### 3. What does `.save()` do? What does `.load()` do? What does `.borrow()` do?

save() saves an object to your account storage.

load() retrieves an object from one's account.

borrow() gets a reference to an object from your account.

#### 4. Explain why we couldn't save something to our account storage inside of a script.

Because scripts do not require the executor's signature and it is not possible to guarantee who executed them. Also, there is no mechanism to prevent multiple executions.

#### 5. Explain why I couldn't save something to your account.

In Flow, the presence of a resource in account storage means that it is owned. Therefore, other people's belongings cannot be tampered with without their permission.

#### 6. Define a contract that returns a resource that has at least 1 field in it. Then, write 2 transactions:

https://play.onflow.org/14705377-4ae2-4d4c-8a06-a3b3f1ef468f?type=account&id=084d637e-18c2-4c6b-9643-d967b0979182&storage=none

```cadence
pub contract MemoContract {
    pub resource Memo {
        pub var content: String

        init(content: String) {
            self.content = content
        }
    }

    pub fun createMemo(content: String): @Memo {
        return <- create Memo(content: content)
    }

    init() {
    }
}
```

i. A transaction that first saves the resource to account storage, then loads it out of account storage, logs a field inside the resource, and destroys it.

```cadence
import MemoContract from 0x01

transaction {
  prepare(signer: AuthAccount) {
    let memo <- MemoContract.createMemo(content: "test memo")
    signer.save(<- memo, to: /storage/Memo)
    let memoLoaded <- signer.load<@MemoContract.Memo>(from: /storage/Memo)!
    log(memoLoaded.content)
    destroy memoLoaded
  }
}
```

ii. A transaction that first saves the resource to account storage, then borrows a reference to it, and logs a field inside the resource.

```cadence
import MemoContract from 0x01

transaction {
  prepare(signer: AuthAccount) {
    let memo <- MemoContract.createMemo(content: "test memo 2")
    signer.save(<- memo, to: /storage/Memo2)
    let memoRef = signer.borrow<&MemoContract.Memo>(from: /storage/Memo2)!
    log(memoRef.content)
  }
}
```

## Day2

#### 1. What does .link() do?

Create a link to a resource object you own that others can call only on a specific interface.

#### 2. In your own words (no code), explain how we can use resource interfaces to only expose certain things to the `/public/` path.

First, create a resource interface that contains only the functions/fields you want to expose. Then, create a resource that implements it. Functions that only you want to perform can call the functions/fields of the resource using the type of the resource as it is. For functions that you want others to perform, specify the resource interface, create a link, and have them use it.

#### 3. Deploy a contract that contains a resource that implements a resource interface. Then, do the following:

https://play.onflow.org/592ae5d6-1940-4db5-b294-06e100097e55?type=account&id=33bdf6e5-6f2a-4b72-b2d3-cde4c0e3f096&storage=none

```cadence
pub contract MemoContract {
    pub resource interface MemoPublic {
        pub var content: String
    }

    pub resource Memo: MemoPublic {
        pub var content: String
        pub var privateContent: String // but actually this is no private in blockchain

        pub fun updateContent(content: String, privateContent: String) {
            self.content = content
            self.privateContent = privateContent
        }

        init(content: String, privateContent: String) {
            self.content = content
            self.privateContent = privateContent
        }
    }

    pub fun createMemo(content: String, privateContent: String): @Memo {
        return <- create Memo(content: content, privateContent: privateContent)
    }

    init() {}
}
```

i. In a transaction, save the resource to storage and link it to the public with the restrictive interface.

```cadence
import MemoContract from 0x01

transaction {
  prepare(signer: AuthAccount) {
    let memo <- MemoContract.createMemo(content: "test memo", privateContent: "test private memo")
    signer.save(<- memo, to: /storage/Memo)
    signer.link<&MemoContract.Memo{MemoContract.MemoPublic}>(/public/Memo, target: /storage/Memo)
  }
}
```

ii. Run a script that tries to access a non-exposed field in the resource interface, and see the error pop up.

<img width="829" alt="ScreenShot 2022-05-21 16 23 03" src="https://user-images.githubusercontent.com/10495516/169640802-54b68b8d-a53a-41fd-b87d-ba4856197647.png">

```cadence
import MemoContract from 0x01

pub fun main(): String {
  let memoRef = getAccount(0x01)
                  .getCapability<&AnyResource{MemoContract.MemoPublic}>(/public/Memo)
                  .borrow() ?? panic("Not Found")
  return memoRef.privateContent
}
```

iii. Run the script and access something you CAN read from. Return it from the script.

```cadence
import MemoContract from 0x01

pub fun main(): String {
  let memoRef = getAccount(0x01)
                  .getCapability<&AnyResource{MemoContract.MemoPublic}>(/public/Memo)
                  .borrow() ?? panic("Not Found")
  log(memoRef.content)
  return memoRef.content
}
```


## Day3

#### 1. Why did we add a Collection to this contract? List the two main reasons.

1. To store multiple NFTs
2. To allow others to deposit NFTs

#### 2. What do you have to do if you have resources "nested" inside of another resource? ("Nested resources")

We must decide what to do with the child resource (destroy it or move it elsewhere) when the parent resource is destroyed.

#### 3. Brainstorm some extra things we may want to add to this contract. Think about what might be problematic with this contract and how we could fix it.

- Idea #1: Do we really want everyone to be able to mint an NFT? 🤔.

A storage-consuming attack vector arises in which a large number of NFTs are minted and deposited into someone's collection. This may be mitigated by setting a mint limit, but it is not perfect.

- Idea #2: If we want to read information about our NFTs inside our Collection, right now we have to take it out of the Collection to do so. Is this good?

This is an operation that can only be performed by the owner of the NFT, and it also unnecessarily increases the computation of the transaction. It is better to create a function to read the NFT information.


## Day4

#### Take our NFT contract so far and add comments to every single resource or function explaining what it's doing in your own words.

```cadence
pub contract CryptoPoops {
  pub var totalSupply: UInt64

  // This is an NFT resource that contains a name, favouriteFood, and luckyNumber
  pub resource NFT {
    pub let id: UInt64

    pub let name: String
    pub let favouriteFood: String
    pub let luckyNumber: Int

    // In initializers, all variables must be explicitly populated with initial values.
    init(_name: String, _favouriteFood: String, _luckyNumber: Int) {
      self.id = self.uuid

      self.name = _name
      self.favouriteFood = _favouriteFood
      self.luckyNumber = _luckyNumber
    }
  }

  // This is a resource interface that allows us to deposit, getIDs and borrowNFT in the Collection.
  pub resource interface CollectionPublic {
    pub fun deposit(token: @NFT)
    pub fun getIDs(): [UInt64]
    pub fun borrowNFT(id: UInt64): &NFT
  }

  // This is a resource for storing NFTs; it provides the ability to deposit and withdraw NFTs.
  // It implements the CollectionPublic interface for others to use.
  pub resource Collection: CollectionPublic {
    pub var ownedNFTs: @{UInt64: NFT}

    // Function to store the NFT in the dictionary that the collection has
    pub fun deposit(token: @NFT) {
      self.ownedNFTs[token.id] <-! token
    }

    // Function to remove NFTs from the dictionaries that the collection has
    pub fun withdraw(withdrawID: UInt64): @NFT {
      let nft <- self.ownedNFTs.remove(key: withdrawID) 
              ?? panic("This NFT does not exist in this Collection.")
      return <- nft
    }

    // Function to get a list of IDs of NFTs that the collection has
    pub fun getIDs(): [UInt64] {
      return self.ownedNFTs.keys
    }

    // Function to get a reference to read the NFT information the collection has
    pub fun borrowNFT(id: UInt64): &NFT {
      return &self.ownedNFTs[id] as &NFT
    }

    // In initializers, all variables must be explicitly populated with initial values.
    init() {
      self.ownedNFTs <- {}
    }

    // In the case of a resource that has resources, the behavior when it itself is destroyed must be explicitly written.
    destroy() {
      destroy self.ownedNFTs
    }
  }

  // Function to create an empty Collection so that you can have an NFT
  pub fun createEmptyCollection(): @Collection {
    return <- create Collection()
  }

  // Only those who have this resource can mint NFTs. It is first stored in the storage of the account that deployed the contract.
  pub resource Minter {
    // Functions for creating NFT resource objects (minting a NFT)
    pub fun createNFT(name: String, favouriteFood: String, luckyNumber: Int): @NFT {
      return <- create NFT(_name: name, _favouriteFood: favouriteFood, _luckyNumber: luckyNumber)
    }

    // Those who have a Minter resource object can also create a new Minter resource object and pass it on to other accounts.
    pub fun createMinter(): @Minter {
      return <- create Minter()
    }
  }

  // In the initializer of the contract, all contract variables must be initialized.
  init() {
    self.totalSupply = 0
    self.account.save(<- create Minter(), to: /storage/Minter)
  }
}
```

