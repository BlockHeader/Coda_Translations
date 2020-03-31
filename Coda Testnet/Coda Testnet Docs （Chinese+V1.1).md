## Coda测试网介绍文档

原文：https://codaprotocol.com/docs/

翻译：Star.LI (star@trapdoortech.com)



# 总览

## Coda协议是什么?

Coda是第一个具有简洁区块链的加密货币协议。像比特币和以太坊加密货币目前存储着数百GB的数据，随着时间的流逝，它们的区块链数据会越来越大。Coda协议，无论多少交易，区块链数据始终保持相同的大小，约20 KB（几条推文的大小）。这意味着可以通过任何设备（包括手机和浏览器）以不信任的方式访问Coda，并可以将Coda协议无缝集成到开发人员的应用程序中。

zk-SNARKs是一种简洁的零知识证明方案，也使Coda协议成为可能。每当Coda节点生成一个新区块时，它还会生成一个新的SNARK证明，以便验证该区块块是否有效。Coda网络中的所有节点都可以存储此证明，并且无需担心区块的原始数据。通过恒定的区块链数据大小，Coda协议可以使网络的吞吐量大大提高，并可以实现可扩展性。

## Coda测试网络

Coda测试网络beta版本已经上线！ 请查看[testnet landing page](https://codaprotocol.com/testnet) 获取更多测试网络的信息，并参与测试网络。

如果你已经准备好运行Coda的测试节点，请查看 [Getting Started page](https://codaprotocol.com/docs/getting-started/) 。



# 入门

欢迎

欢迎来到[Coda Genesis计划](https://codaprotocol.com/genesis)的申请者！  测试网的第三阶段测试网已启动！ 我们将在[Coda Discord服务器](https://bit.ly/CodaDiscord)上的#announcements频道以及通过电子邮件发布更多公告。

**注册获取抵押代币**-[在此处注册](http://bit.ly/StakingSignup)，以接收抵押代币，加入测试网。 区块生产者（拥有Coda并参与共识的节点）是Coda网络的组成部分，而生产区块将帮助您赢得测试网挑战并积累测试网积分。 如果您对在测试网上注册有任何疑问，请与Discord服务器联系。

本节说明在本地计算机上运行Coda协议节点并连接到网络所需的要求。

注意

本文档适用于**beta**版本。 初始发行版之前，命令和API可能会更改。 最新的版本是“ 0.0.12-beta”。

## 软硬件要求

**软件**: macOS 或者 Linux （目前支持 Debian 9 和 Ubuntu 18.04 LTS）

注意：目前不支持Windows。 但是，社区成员成功在Windows系统上运行Linux，并运行节点。 单击[此处](https://forums.codaprotocol.com/t/unofficial-wsl-instructions/26)，获取社区创建的Windows节点的使用说明。

**硬件**：发送和接收Coda不需要任何特殊硬件，但是在Coda网络上运行区块生产节点目前需要：

- 最低4核CPU
- 最少8G内存

注意的是：如果你打算运行snark worker节点，则需要更多的内存 - 推荐使用16GB。GPU目前并不要求，但有可能后面协议升级需要。

**网络**: 最少1 Mbps带宽

**虚拟机实例**：O(1)Labs已在多个云主机平台上测试了运行节点，并为基本的节点需求推荐了以下实例。 请记住，自定义要求以及不同的成本约束可能需要不同的实例类型。

- AWS - [c5.2xlarge](https://www.ec2instances.info/?filter=c5.2xl&region=us-west-2&cost_duration=daily&selected=c5.2xlarge)
- GCP - [c2-standard-4](https://cloud.google.com/compute/docs/machine-types)
- Azure - [Standard_F8s_v2](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sizes-compute#fsv2-series-1)
- Digital Ocean - [c-8-16gib](https://cloud.digitalocean.com/droplets/new?size=c-8-16gib)

## 安装

提供了针对macOS和Linux的安装说明。可执行文件比较大，大约1GB，因此安装可能需要一些时间。

警告

如果您安装了老的版本`coda`，则需要对其进行升级，以免因使用较旧的客户端而连接不上网络的问题。 请参阅以下说明升级macOS和Linux可执行程序。

## macOS

使用 [Homebrew](https://brew.sh/)安装

```
brew install codaprotocol/coda/coda
```

如果您已经安装了旧版本，请运行：

```
brew upgrade coda
```

您可以运行 `coda -help` 确认安装是否成功。

## Ubuntu 18.04 / Debian 9

添加Coda Debian源，并安装：

```
sudo apt-get remove coda-testnet-postake-medium-curves
sudo apt-get remove coda-kademlia
echo "deb [trusted=yes] http://packages.o1test.net release main" | sudo tee /etc/apt/sources.list.d/coda.list
sudo apt-get update
sudo apt-get install -t release coda-testnet-postake-medium-curves
```

如果您安装了老的版本，通过上述命令，可以自动删除老版本并安装新版本。如果你第一次运行第一个命令，你会发现错误，E: Unable to locate package coda-testnet-postake-medium-curves`。请忽略该错误，该错误只是说明没有安装过Coda执行程序。

您可以运行 `coda -help` 确认安装是否成功。

## Windows

目前不支持Windows系统。如果你对支持Windows感兴趣，请联系support@o1labs.org或者通过[Discord server](https://bit.ly/CodaDiscord)沟通。

## 从源代码编译

如果你的系统是不同的Linux发行版本，或者不同的Mac OS版本，请查看 [try building Coda from source code](https://github.com/CodaProtocol/coda/blob/master/README-dev.md#building-coda)，从源代码编译可执行程序。注意的是，其他操作系统并没有充分测试，有可能存在问题。如遇问题，请通过Discord分享和寻求帮助。

## 设置端口和防火墙

如果您正在运行防火墙，则应允许8303端口的TCP数据通讯。此外，除非提供了“ -external-ip YOUR_IP”选项，否则守护程序将使用HTTPS（443）和HTTP（80）尝试确定自己的IP地址。

您可能需要配置路由器的端口转发，以允许通过您的**外部** IP地址到以下端口的入站流量。

- `TCP` 端口 `8302` 和 `8303`

其他说明，请查看 [this guide](https://codaprotocol.com/docs/troubleshooting/#port-forwarding)。

## 下一节

目前，你已经安装好Coda并设置好了网络，接下来是更有趣的事情 - [发送交易](https://codaprotocol.com/docs/my-first-transaction/)！



# 第一个交易

在本节中，我们将在Coda网络上进行第一笔交易。 [安装软件](https://codaprotocol.com/getting-started)之后，我们需要先创建一个新帐户，然后才能发送或接收Coda。 让我们首先启动节点。

## 启动节点

运行以下命令以启动Coda节点并连接到网络：

```
coda daemon \
    -discovery-port 8303 \
    -peer /dns4/seed-one.genesis.o1test.net/tcp/10002/ipfs/12D3KooWP7fTKbyiUcYJGajQDpCFo2rDexgTHFJTxCH8jvcL1eAH \
    -peer /dns4/seed-two.genesis.o1test.net/tcp/10002/ipfs/12D3KooWL9ywbiXNfMBqnUKHSB1Q1BaHFNUzppu6JLMVn9TTPFSA
```

上面指定的主机和端口是指种子地址。 由于Coda是[peer-to-peer](https://codaprotocol.com/glossary/#peer-to-peer)协议，因此我们不依赖任何单一的中心化服务器。 如果使用了自定义端口（TCP的不是8303），则需要向上面的命令传递一个额外的选项：`-external-port`。

注意

每当您使用`coda client`发出命令时，守护进程都需要运行，因此请确保不要意外杀死守护进程。

首次运行节点时的常见问题，请参见[常见问题](https://codaprotocol.com/docs/troubleshooting/)。

## 查看网络连接

现在我们已经启动了一个节点并正在运行Coda守护程序，打开另一个终端并运行以下命令：

```
coda client status
```

注意

目前，`coda client status`在首次启动时可能需要一分钟才能连接到守护程序。 因此，如果您看到“错误：守护程序未运行，请查看coda守护程序是否运行”，稍等片刻重试。

我们很可能会看到包含以下字段的回复：

```
...
Peers:                                         Total: 4 (...)
...
Sync Status:                                   Bootstrap
```

如果您看到`Sync Status: Bootstrap`，则表示Coda节点正在启动，需要与网络的其余部分进行同步。 您可能需要耐心等待，因为此步骤可能需要一些时间才能使节点获取所需的所有数据。 当同步状态达到`Synced`并且该节点连接到1个或多个对等节点时，我们才成功连接到网络。

## 创建账户

节点同步后，我们将创建一个公钥/私钥对，以便我们可以交易签名，以及生成一个地址以接收付款。 出于安全原因，我们希望将密钥放在攻击者更难以访问的目录下。

运行以下任意一个命令，将在当前目录的`keys`子目录下创建一个公共和私有密钥`my-wallet`和`my-wallet.pub`：

```
coda client-old generate-keypair -privkey-path keys/my-wallet 

coda accounts create
```

警告

公钥可以分享给任何人， 但切勿与任何人共享私钥，因为它等同于您的资金密码。

```
Keypair generated
Public key:  4vsRCVbLm6LvUyzYWT95WaCzyi4D4UHxRpLBhMn7q2mRPgNCgRG3Jr3tDuhgQdmzbvCcBxhUwB3REpY2Dyf1NAxSSs8Q2vdJX93pT7eyqcyRU2S9UpDddDgovj46BSknNjzydKoopebp5Kva
```

由于公钥很长且难以记住，因此将其保存为环境变量：

```
export CODA_PK=<public-key>
```

现在我们可以在任何地方以`$ CODA_PK`的形式访问它。 请注意，这只会保存到当前的终端会话中，因此，如果要保存它以备将来使用，可以将其添加到您的`~/.profile`或`~/.bash_profile`中。

## 获取测试Coda

为了发送第一笔交易，我们首先需要获取一些Coda。 转到[Coda Discord服务器](https://bit.ly/CodaDiscord)并加入“ #faucet”频道。 向Tiny的机器人索要一些Coda（您将收到100个Coda）。 命令如下：

```
$request <public-key>
```

一旦批准了您的请求，请密切关注Discord渠道以查看交易何时进行。 您的资金可能要过几分钟才能显示。

我们可以通过运行以下命令并输入公钥来检查余额，以确保我们收到了资金：

```
coda client get-balance -public-key $CODA_PUBLIC_KEY
```

您可能会看到`No account found at that public_key (zero balance)`。 耐心等待！ 根据网络中的交易情况，可能需要花费一些时间才能完成交易。

在等待期间，请运行以下命令以查看当前区块的高度：

```
coda client status
```

## 转账

最后，我们可以发送了第一笔交易！ 为了进行测试，我们已经设置了[自动退回服务](https://github.com/CodaProtocol/coda-automation/tree/master/services/echo)，该应用将立即退还您的付款（扣除了交易费用）。

警告

目前，自动退回服务存在一个已知问题，导致其无法正确退回您的付款！ 不用担心，我们仍然会为您提供Testnet积分[*]（https://codaprotocol.com/docs/my-first-transaction#disclaimer），以完成挑战。

让我们转账给自动退回服务。命令类似：

```
coda client send-payment \
  -amount 20 \
  -receiver 4vsRCVNep7JaFhtySu6vZCjnArvoAhkRscTy5TQsGTsKM4tJcYVc3uNUMRxQZAwVzSvkHDGWBmvhFpmCeiPASGnByXqvKzmHt4aR5uAWAQf3kqhwDJ2ZY3Hw4Dzo6awnJkxY338GEp12LE4x \
  -fee 5 \
  -sender $YOUR_PUBLIC_KEY
```

上述命令中的参数为：

- `amount`，交易金额（20 Coda）
- `receiver`， [自动退回服务地址](https://github.com/CodaProtocol/coda-automation/tree/master/services/echo)
- `fee`，交易手续费
- `sender`，交易发送方

如果上述交易发送成功，会收到如下的回复信息：
```
Dispatched payment with ID 3XCgvAHLAqz9VVbU7an7f2L5ffJtZoFega7jZpVJrPCYA4j5HEmUAx51BCeMc232eBWVz6q9t62Kp2cNvQZoNCSGqJ1rrJpXFqMN6NQe7x987sAC2Sd6wu9Vbs9xSr8g1AkjJoB65v3suPsaCcvvCjyUvUs8c3eVRucH4doa2onGj41pjxT53y5ZkmGaPmPnpWzdJt4YJBnDRW1GcJeyqj61GKWcvvrV6KcGD25VEeHQBfhGppZc7ewVwi3vcUQR7QFFs15bMwA4oZDEfzSbnr1ECoiZGy61m5LX7afwFaviyUwjphtrzoPbQ2QAZ2w2ypnVUrcJ9oUT4y4dvDJ5vkUDazRdGxjAA6Cz86bJqqgfMHdMFqpkmLxCdLbj2Nq3Ar2VpPVvfn2kdKoxwmAGqWCiVhqYbTvHkyZSc4n3siGTEpTGAK9usPnBnqLi53Z2bPPaJ3PuZTMgmdZYrRv4UPxztRtmyBz2HdQSnH8vbxurLkyxK6yEwS23JSZWToccM83sx2hAAABNynBVuxagL8aNZF99k3LKX6E581uSVSw5DAJ2S198DvZHXD53QvjcDGpvB9jYUpofkk1aPvtW7QZkcofBYruePM7kCHjKvbDXSw2CV5brHVv5ZBV9DuUcuFHfcYAA2TVuDtFeNLBjxDumiBASgaLvcdzGiFvSqqnzmS9MBXxYybQcmmz1WuKZHjgqph99XVEapwTsYfZGi1T8ApahcWc5EX9
Receipt chain hash is now A3gpLyBJGvcpMXny2DsHjvE5GaNFn2bbpLLQqTCHuY3Nd7sqy8vDbM6qHTwHt8tcfqqBkd36LuV4CC6hVH6YsmRqRp4Lzx77WnN9gnRX7ceeXdCQUVB7B2uMo3oCYxfdpU5Q2f2KzJQ46
```

## 查看余额

现在我们可以发送交易了。让我们通过运行以下命令来检查当前余额。查询余额时，需要提供查询帐户的公钥：

```
coda client get-balance -public-key $CODA_PK
```

查询回复类似：

```
Balance: 50 coda
```

一旦您对创建地址以及发送和接收Coda熟练后，我们就可以进入Coda网络真正独特的部分-[参与共识并帮助压缩区块链](https://codaprotocol.com /docs/node-operator)。

\*_Testnet积分仅用于跟踪对Testnet的贡献情况，Testnet积分没有现金或其他货币价值。 Testnet点不可转让，不可兑换或交换任何加密货币或数字资产。 我们可以随时修改或取消Testnet积分。_


# 成为节点

危险提示

节点操作命令仍处于稳定状态，因此这些命令可能会更改。 请尝试并提交任何修复。

现在我们已经设置了Coda节点并发送了第一笔交易，让我们将注意力转移到其他可以与Coda网络进行交互的方法上，即参与共识，并通过生成zk-SNARK来帮助压缩数据。 通过运行有助于保护网络安全的节点，您将获得Coda作为奖励。

## 参与共识

Coda网络采用[POS共识](https://codaprotocol.com/docs/glossary/#proof-of-stake) 。 采用POS共识算法，您不需要像比特币采矿那样拥有复杂的计算机设备。 通过简单地将Coda放入我们的钱包中，我们可以选择将其委托给自己或者其他节点。 首先让我们看看如何委托Coda：

## 抵押Coda

通过[发送交易](https://codaprotocol.com/docs/my-first-transaction)，我们获取了一些Coda，因此我们现在可以使用`-propose-key`选项在启动守护进程时抵押Coda。 先停止当前的守护进程，并使用以下命令重新启动它，设置存储私钥的路径（我们之前在`keys/my-wallet`中创建了密钥对）：

```
coda daemon \
    -discovery-port 8303 \
    -peer /dns4/seed-one.genesis.o1test.net/tcp/10002/ipfs/12D3KooWP7fTKbyiUcYJGajQDpCFo2rDexgTHFJTxCH8jvcL1eAH \
    -peer /dns4/seed-two.genesis.o1test.net/tcp/10002/ipfs/12D3KooWL9ywbiXNfMBqnUKHSB1Q1BaHFNUzppu6JLMVn9TTPFSA \
    -propose-key keys/my-wallet
```

注意

你可以提供多个私钥存储路径，同时完成多个抵押。

可以通过`coda client status` 命令查看抵押情况：

```
coda client status

Coda Daemon Status 
-----------------------------------

Global Number of Accounts:                     18
The Total Number of Blocks in the Blockchain:  1
Local Uptime:                                  36s
Ledger Merkle Root:                            ...
Staged-ledger Hash:                            ...
Staged Hash:                                   ...
GIT SHA1:                                      ...
Configuration Directory:                       ...
Peers:                                         ...
User_commands Sent:                            0
Snark Worker Running:                          false
Sync Status:                                   Offline
Proposers Running:                             Total: 1 (8QnLUNW7sUxnApau4SLShwr25koiSKrECxtveu89PPmQW5pEyy3xK8YgRpZQkZEanc)
Best Tip Consensus Time:                       0:0
Consensus Time Now:                            11542:461
Consensus Mechanism:                           proof_of_stake
...
```

其中，`Proposers Running`指定抵押的账户信息。

警告

请记住，如果您抵押给自己，则需要始终保持与网络的连接，因为你的节点会被选为出块节点。 如果您需要经常下线，最好抵押给其他节点。

## 委托 coda

委派Coda是直接抵押的另外一个选择，其好处是不必始终保持与网络的连接。 但是，请记住：

- 更改委托，您将需要支付少量交易费用，因为更改委托也是一种交易
- 您委托的节点可以选择向您收取佣金

委托需要执行如下的命令：

```
coda client delegate-stake \
    -delegate <delegate-public-key> \
    -privkey-path <file> \
    -fee <fee>
```

命令中的参数为：

- `delegate`，委托节点的公钥信息
- `privkey-path` ，是自己的存储私钥的路径
- `fee` ，交易费用

在如下情况下，可以进行委托：

- 从“冷钱包”中，给自己的节点进行委托
- 委托给“抵押池”，获取周期性的收益

注意

此更改生效之前有一天的等待期，以防止滥用网络。

## 数据压缩

Coda协议的独特之处在于，它不需要节点像其他加密货币协议一样维护区块链的完整历史记录。 通过递归证明，Coda协议有效地将区块链压缩到恒定大小。 我们称其为压缩，因为它可以将TB的数据减少到几千字节。

但是，这不是传统意义上的数据编码或压缩，而是节点通过生成零知识证明来“压缩”网络中的数据。 节点在此过程中扮演着至关重要的角色，他们将自己指定为“ snark-worker”，为已添加到区块中的交易生成zk-SNARK证明。

当 [启动守护进程](https://codaprotocol.com/docs/my-first-transaction/#start-up-a-node)时，设置其他的参数启动“snark-worker”：

```
coda daemon \
    -discovery-port 8303 \
    -peer /dns4/seed-one.genesis.o1test.net/tcp/10002/ipfs/12D3KooWP7fTKbyiUcYJGajQDpCFo2rDexgTHFJTxCH8jvcL1eAH \
    -peer /dns4/seed-two.genesis.o1test.net/tcp/10002/ipfs/12D3KooWL9ywbiXNfMBqnUKHSB1Q1BaHFNUzppu6JLMVn9TTPFSA \
    -run-snark-worker $CODA_PK \
    -snark-worker-fee <fee>
```
作为“snark-worker”，可以获取一部分区块奖励。 区块生产者负责收集交易，并且按照协议奖励snark-worker。

该节内容涵盖了作为Coda节点的角色和职责。 由于Coda是一个无需许可的点对点网络，因此Coda协议由世界各地的节点以分散的方式进行管理和运行。 同样，Coda项目也是分布式的，无需许可即可加入。 Coda协议的代码都是开源的，并且有很多工作要做，无论是技术性的还是非技术性的。 要了解有关如何参与Coda的更多信息，请查看[如何贡献](https://codaprotocol.com/contributing)。
