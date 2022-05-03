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

`AuthAccount` is an object to access the account's storage of the authorizer of a transaction. Using its methods, it is possible to store resource objects and create links to the account's storage.

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

