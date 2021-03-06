---

layout: post
title: "区块链入门"
date: 2017-11-18
description: "区块链入门"
tag: 区块链 

---

   这篇文章主要基于中本聪的《[Bitcoin: A Peer-to-Peer Electronic Cash System](https://bitcoin.org/bitcoin.pdf)》。

   区块链技术可以追溯到数十年前，但是2008年中本聪发表的比特币原始论文提出一种基于区块链的项目——比特币，因为其创新和可实现让这种货币和它的底层技术——区块链一起带火起来。中本聪的这篇论文着重讲述网络结构，公式较少，尝试用现代技术去完成去中心化的网络体系，更像是一篇蓝图，阅读起来并不困难所以推荐阅读原文。

## 简介

比特币是一种区别于我们平时使用的第三方支付（比如微信、支付宝）的货币。后者虽然是电子化的货币，但仍然需要权威的第三方介入，与现实中使用的现金缺少匿名性（交易双方无需知道对方信息）和线下交易能力（无需第三方验证）。引入可信第三方的好处有很多，诸如对货币进行验证、保证流通量可知（毕竟账本在第三方那），在国家层面还能查洗钱。另外，在虚拟世界如果去掉第三方还会产生数字货币被轻易复制的问题，也称“Double-Spending”。总的来说，比特币需要解决三个问题：匿名性、线下交易以及double-spending，区块链就是支撑比特币的底层技术。

## 交易

通过前面的论述我们可以看到，为了去掉可信第三方，比特币网络需要解决验证货币和double-spending等问题，一个解决的办法就是**公开账本**。

其实银行等第三方机构承担的就是记账本的功能，通过一个总账本，即可防止货币被复制、假冒。账本的一个单元就是交易。在交易时，交易双方（A和B）中A付给B 10元，则A解锁10元系统减少10元并生成只有B能解锁的新的10元。这里就涉及到加密、解密，B可以通过数字签名验证这笔钱的真伪。如下图

![](/images/posts/blockchain/transactions.png)

但是这里还没有解决double-spending的问题，即B验证了这笔钱是真的但是无法知道之前是否使用过。怎么解决呢，一个可行的办法就是每个交易加上时间戳。同时后面也将看到，加上时间戳也能防止账本被篡改。

## 工作量证明

前面说到公开账本，一个关键问题就是账本的公信力问题，也就是需要大部分人都承认这个账本是可信的、无法篡改的。为了达到这个目的，一个简单办法就是利用哈希函数的性质。把某个时间段内的若干条交易记录的简单集合称为区块。在区块内把不同的交易分别生成哈希值，随后又生成联合哈希值，最后得到如下图的Merkle树。

![](/images/posts/blockchain/Merkle.png)

由于哈希函数的性质，只要一个交易发生了改变，哈希函数即改变，同时加上时间戳，使交易时间可以确定，保证交易记录无法篡改。另外使用哈希的方式同时也能够有效节省存储空间，假设一个区块header大小为80字节，10分钟产生一个区块，则1年所需要的空间大小为  80 byte * 6 * 24 * 365 = 4.2MB，相对于现代设备来说几乎可以忽略。

当需要验证某个交易是否存在时，可以对该交易生成哈希值然后沿着Merkle树往上追溯，如果与root hash一致则说明存在。这样就免去了查找全网节点的必要，所以又称“**Simplified Payment Verification**”。如下图：

![](/images/posts/blockchain/simplifiedPV.png)

现在一切都很完美，那么如果有人要把交易记录进行篡改呢？让我们来分析一下。我们知道，当攻击者修改某个交易记录时，对应的哈希值会发生改变，进而新的Merkle树的root hash就会发生改变。又因为区块链是把区块连接形成一个链条，这个区块发生改变会使得后面所有区块哈希值都改变。对于两条不同的链条，一般认为最长链为可信的，所以攻击者的链条就需要与真实的链条进行一场比赛。为了产生一个新的区块，要求这个区块的哈希值满足相应的条件，这就需要计算机不停地计算，直到网络中某个节点的计算机首先计算出满足条件的区块并通过网络传播出去，这个过程就是**工作量证明**，为了激励其他节点进行计算，产生区块的节点会有相应奖励，就像挖矿工人在挖矿。所以，如果要成功修改交易记录，攻击者产生区块速度就必须比真实链条速度快，也就是攻击者需要占有超过全网50%的算力，这种情况按照中本聪的设想一般不会出现。