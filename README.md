# vns-stratum-miner

使用golang编写的vns挖矿软件，将原官方的getwork协议改成了stratum。**无开发者税**

## 对比getwork

stratum是基于tcp的协议，首先由于其不带有http的header，每条数据大约能够节省矿池端入带宽（挖矿端出）**20%~40%流量**，矿池端出带宽（挖矿端入）的**30%~50%的流量**。

其次，getwork不带有订阅功能，很容易在快速挖矿环境（如vns10s出块）下造成过期任务。对此官方软件实现是在极短间隔内getwork，这明显会对pool形成flood，这也是造成官池经常宕机原因————根本不用别人ddos它它自己就已经撑不住了。

而stratum由于其tcp协议，可以实现矿池在发现新高度后主动向挖矿端推送新任务，无需挖矿端反复请求。保证了当前任务绝对正确，**增加有效提交，让算力更有价值。**

## 软件优势

本软件有两个版本
- golang + c/c++
- pure golang with ASM

不同环境下算力有所差距。

## 使用要求

矿池端必须开启stratum！

如需矿池软件请至此https://github.com/maoxs2/vnsPool

## 源码

欢迎golang大神来审查源码，请邮件私聊

## 另

**无开发者税**，完全懒得写抽税代码。

## 使用方法

```bash
$ ./vnsMiner -h
Welcome using vnsMiner, written by Command (https://github.com/maoxs2)
  -c int
        core number (default 12)
  -h    get help page
  -o string
        pool address, e.g 127.0.0.1:8008
  -t uint
        thread number
  -u string
        username/address for pool mining (default "0x0")

```

`vnsMiner -c [coreNumber] -o [poolIP:poolPort] -t [threadNumber] -u [address]`
