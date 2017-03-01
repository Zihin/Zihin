---
layout:     post
title:      "Definition of statistic in ethstats.net"
tags:       [Blockchain, Ethereum]
categories: [Blockchain]
---

The precise definition of each statistic and graph displayed in
[https://ethstats.net](https://ethstats.net).


![](http://upload-images.jianshu.io/upload_images/1218580-78f41504d4745861.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


**Best Block** is the *heaviest* block regarding the cummultative difficulty, or in simple words: the highest block number of the longest valid chain.
**Uncles** are orphaned blocks, but in oposite to other blockchain systems, [uncles are rewarded](http://ethereum.stackexchange.com/q/34/87) and included in the blockchain. Shows current bloc's uncle count and uncle count of last 50 blocks.
**Last Block** shows the time since the last block was mined, usually in seconds.
**Average Block Time** is, well, the average time between two blocks, excluding uncles, in seconds. Should be something around 15 seconds.
**Average Network Hashrate** is the number of hashes bruteforced by the network miners to find a new block. 5 TH/s means the network power is at *five trillion* hashes per second.
**Difficulty** is the current [mining difficulty](http://ethereum.stackexchange.com/q/1880/87) to find a new block which basicly means how hard it is to find a matching hash.
**Active Nodes** is the number of connected nodes to the Ethstats dashboard, (not the whole ethereum network!)
**Gas Price** is the price miners accept for gas. While gas is used to calculate fees. 20 gwei is the current default, which stands for 20 Giga-Wei which are *twenty billion wei* that is 0.00000002 ETH.
**Gas Limit** is the block gas limit. It defaults to 1.5 pi million gas (4,712,388) and miner can only include transactions until the gas limit is met (and the block is *full*). The gas limit is the analogy to bitcoin's block size limit, but not fixed in size.
**Page Latency** and **Uptime** are specific stats for the dashboard.
**Block Time Chart** shows the actual time between the last blocks.
**Difficulty Chart** shows the actual difficulty of the last blocks.
**Block Propagation Chart** shows how fast blocks are shared among the nodes connected to the dashboard.
**Last Block Miners** are the public keys of the miners who found most of the last blocks.
**Uncle Count Chart** shows numbers of uncles per 25 blocks per bar.
**Transactions Chart** shows numbers of transactions included in last blocks.
**Gas Spending Chart** shows how much gas was spent on transactions in each block, note the correlation to the transactions chart.
**Gas Limit Chart** shows the dynamicly adjusted block gas limit for each block.
