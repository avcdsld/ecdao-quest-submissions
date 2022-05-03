0x4c9135af735b894d

# [Chapter1](https://github.com/emerald-dao/beginner-cadence-course/tree/main/chapter1.0)

## Day1

### 1. Explain what the Blockchain is in your own words.

ブロックチェーンは、公共の場所に存在する石版のようなもの。
暗号学的な鍵でアイデンティティを示すことで、誰でも情報を書き込んだり、読むことができる。
基本的な機能として、誰にいくらを送金するという意思を書き込むことで、送金システムが実現されている。
また、そこにはコンピュータプログラムも記録することができる。

A blockchain is like a lithography that exists in a public place.
Anyone can write or read the information by indicating their identity with a cryptographic key.
The basic function of a money transfer system is to write the intention to send money to whom and how much.
Computer programs can also be recorded there.

### 2. Explain what a Smart Contract is.

スマートコントラクトは、ブロックチェーン上に記録されたコンピュータプログラムである。
そこに書かれたルールに従って、多様なデジタル資産や創造物を構築できる。

A smart contract is a computer program recorded on a blockchain.
According to the rules written there, a wide variety of digital assets and creations can be constructed.

### 3. Explain the difference between a script and a transaction.

スクリプトは、ブロックチェーンの情報を読み取るためのコード。無料で実行できる。
トランザクションは、ブロックチェーンの情報を書き換えてインタラクションするためのコード。こちらは手数料がかかる。

Script is code for reading blockchain information. It can be executed for free.
Transaction is the code to rewrite the blockchain information and interact with the blockchain. There is a fee for this.


## Day2

### 1. What are the 5 Cadence Programming Language Pillars?

- Safety and Security
- Clarity
- Approachability
- Developer Experience
- Resource Oriented Programming

### 2. In your opinion, even without knowing anything about the Blockchain or coding, why could the 5 Pillars be useful (you don't have to answer this for #5)?

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

### 1. Deploy a contract to account `0x03` called "JacobTucker". Inside that contract, declare a **constant** variable named `is`, and make it have type `String`. Initialize it to "the best" when your contract gets deployed.

https://play.onflow.org/70008c75-5567-4b28-84b8-1298ac6fb6a1?type=account&id=e95c5ef8-066d-4797-94a3-dfe6f0562449&storage=none

```cadence
pub contract JacobTucker {
    pub let is: String

    init() {
        self.is = "the best"
    }
}
```

### 2. Check that your variable `is` actually equals "the best" by executing a script to read that variable. Include a screenshot of the output.
<img width="1124" alt="ScreenShot 2022-05-03 16 46 18" src="https://user-images.githubusercontent.com/10495516/166419921-8b27819d-26cb-41cb-a3da-b489d1d0c7f0.png">
