# 前言

区块链作为一种架构设计的实现，与基础语言或平台等差别较大。区块链是加密货币背后的技术，是当下与VR虚拟现实等比肩的热门技术之一，本身不是新技术，类似Ajax，可以说它是一种技术架构，所以我们从架构设计的角度谈谈区块链的技术实现。

无论你擅长什么编程语言，都能够参考这种设计去实现一款区块链产品。与此同时，梳理与之相关的知识图谱和体系，帮助大家系统的去学习研究。

# 基本概念

区块链的概念最近很火，它来自于比特币等加密货币的实现，但是目前，这项技术已经逐步运用在各个领域。什么是区块链技术？为了感性认识这个问题，我们可以使用谷歌地球的例子做类比，ajax不是什么新技术，但组合在一起就成就了产品谷歌地球，与之类似，区块链也不是什么新技术，但与加密解密技术、P2P网络等组合在一起，就诞生了比特币。技术人员，特别是Web开发工程师，学习了解ajax技术最早是被谷歌地球酷炫的效果所吸引。而现在，历史再一次重演，很多人被比特币的疯狂发展所吸引，进而开始研究其背后的技术——区块链。

区块链原本是比特币等加密货币存储数据的一种独特方式，是一种自引用的数据结构，用来存储大量交易信息，每条记录从后向前有序链接起来，具备公开透明、无法篡改、方便追溯的特点。实际上，这种特性也直接体现了整个比特币的特点，因此使用区块链来概括加密货币背后的技术实现是非常直观和恰当的。区块链是一项技术，加密货币是其开发实现的一类产品（含有代币，也有不含代币的区块链产品），不能等同或混淆。与加密货币相比，区块链这个名字抛开了代币的概念，更加形象化、技术化、去政治化，更适合作为一门技术去研究、去推广。

所以，目前当大家单独说到区块链的时候，就是指的区块链技术，是实现了数据公开、透明、可追溯的产品的架构设计方法，算作广义的区块链。而当在具体产品中谈到区块链的时候，可以指类似比特币的数据存储方式，或许是数据库设计，或许是文件形式的设计，这算作狭义的区块链。广义的区块链技术，必须包含点对点网络设计、加密技术应用、分布式算法的实现、数据存储技术的使用等4个方面，其他的可能涉及到分布式存储、机器学习、VR、物联网、大数据等。狭义的区块链仅仅涉及到数据存储技术，数据库或文件操作等。本文的区块链，指的是广义的区块链。

# 架构图

从架构设计上来说，区块链可以简单的分为三个层次，协议层、扩展层和应用层。其中，协议层又可以分为存储层和网络层，它们相互独立但又不可分割。如图：

 [![区块链架构图](/img/blockchain_overview.png "区块链架构图")](https://github.com/MinuteBook/blockchain/blob/master/img/blockchain_overview.png?raw=true)
 
 # 协议层
 
 所谓的协议层，就是指代最底层的技术。这个层次通常是一个完整的区块链产品，类似于我们电脑的操作系统，它维护着网络节点，仅提供Api供调用。通常官方会提供简单的客户端（通称为钱包），这个客户端钱包功能也很简单，只能建立地址、验证签名、转账支付、查看余额等。这个层次是一切的基础，构建了网络环境、搭建了交易通道、制定了节点奖励规则，至于你要交易什么，想干什么，它一概不过问，也过问不了。典型的例子，自然是比特币，还有各种二代币，比如莱特币等，本书介绍的亿书币也是。这个层次，是现阶段开发者聚集的地方，这说明加密货币仍在起步当中。

从用到的技术来说，协议层主要包括网络编程、分布式算法、加密签名、数据存储技术等4个方面，其中网络编程能力是大家选择编程语言的主要考虑因素，因为分布式算法基本上属于业务逻辑上的实现，什么语言都可以做到，加密签名技术是直接简单的使用（请看书中相关的加密解密文章，不建议自由发挥，没有过多的编码逻辑），数据库技术也主要在使用层面，只有点对点网络的实现和并发处理才是开发的难点，所以对于那些网络编程能力强，对并发处理简单的语言，人们就特别偏爱。也因此，Nodejs开发区块链应用，逐渐变得更加流行，Go语言也在逐渐兴起。

上面的架构设计图里，我把这个层面进一步分成了存储层和网络层。数据存储可以相对独立，选择自由度大一些，可以单独来讨论。选择的原则无非是性能和易用性。我们知道，系统的整体性能，主要取决于网络或数据存储的I/O性能，网络I/O优化空间不大，但是本地数据存储的I/O是可以优化的。比如，比特币选择的是谷歌的LevelDB，据说这个数据库读写性能很好，但是很多功能需要开发者自己实现。目前，困扰业界的一个重大问题是，加密货币交易处理量远不如现在中心化的支付系统（银行等），除了I/O，需要全方位的突破。

分布式算法、加密签名等都要在实现点对点网络的过程中加以使用，所以自然是网络层的事情，也是编码的重点和难点，《Nodejs开发加密货币》全书分享的基本上就是这部分的内容。当然，也有把点对点网络的实现单独分开的，把节点查找、数据传输和验证等逻辑独立出来，而把共识算法、加密签名、数据存储等操作放在一起组成核心层。无论怎么组合，这两个部分都是最核心、最底层的部分，都是协议层的内容。

# 扩展层

这个层面类似于电脑的驱动程序，是为了让区块链产品更加实用。目前有两类，一是各类交易市场，是法币兑换加密货币的重要渠道，实现简单，来钱快，成本低，但风险也大。二是针对某个方向的扩展实现，比如基于亿书侧链，可为第三方出版机构、论坛网站等内容生产商提供定制服务等。特别值得一提的就是大家听得最多的“智能合约”的概念，这是典型的扩展层面的应用开发。所谓“智能合约”就是“可编程合约”，或者叫做“合约智能化”，其中的“智能”是执行上的智能，也就是说达到某个条件，合约自动执行，比如自动转移证券、自动付款等，目前还没有比较成型的产品，但不可否认，这将是区块链技术重要的发展方向。

扩展层使用的技术就没有什么限制了，可以包括很多，上面提到的分布式存储、机器学习、VR、物联网、大数据等等，都可以使用。编程语言的选择上，可以更加自由，因为可以与协议层完全分离，编程语言也可以与协议层使用的开发语言不相同。在开发上，除了在交易时与协议层进行交互之外，其他时候尽量不要与协议层的开发混在一起。这个层面与应用层更加接近，也可以理解为B/S架构的产品中的服务端（Server）。这样不仅在架构设计上更加科学，让区块链数据更小，网络更独立，同时也可以保证扩展层开发不受约束。

从这个层面来看，区块链可以架构开发任何类型的产品，不仅仅是用在金融行业。在未来，随着底层协议的更加完善，任何需要第三方支付的产品都可以方便的使用区块链技术；任何需要确权、征信和追溯的信息，都可以借助区块链来实现。我个人觉得，这个目标应该很快就能实现。

# 应用层

这个层面类似于电脑中的各种软件程序，是普通人可以真正直接使用的产品，也可以理解为B/S架构的产品中的浏览器端（Browser）。这个层面的应用，目前几乎是空白。市场亟待出现这样的应用，引爆市场，形成真正的扩张之势，让区块链技术快速走进寻常百姓，服务于大众。大家使用的各类轻钱包（客户端），应该算作应用层最简单、最典型的应用。很快，亿书将基于亿书网络推出文档协作工具，这个就是典型的应用层的产品。

限于当前区块链技术的发展，亿书只能从协议层出发，把目标指向应用层，同时为第三方开发者提供扩展层的强大支持。这样做既可以避免贪多，又可以避免无法落地，是真正理性的开发路线。因为纯粹的开发协议层或扩展层，无法真正理解和验证应用层，会脱离实际，让第三方开发者很难使用。如果仅仅考虑应用层，市面上又找不到真正牢固、易用的协议层或扩展层的产品。所以，我们只好全面发力，采取完全开源开放的态度，通过社区的力量，共同去做一件有意义的事情，也算为中国区块链技术发展做点技术积累和微薄贡献。

# 编程实现

很多小伙伴，习惯结合自己的技术背景，来理解上面的架构设计。这里，结合具体的编程语言，简单介绍几款产品，仅供参考。

 1. C/C++
 
    这两个语言是无法逾越的，任何开发遇到瓶颈，基本上都会找到它们，自然应该排在第一位要介绍的。同时，区块链技术的鼻祖，比特币（协议层）就是用C++语言开发的，而且目前为止，没有比比特币更加成功的区块链产品。所以，无论你使用什么语言开发，在正式进入这个行业的过程中，都应该先研究研究比特币。比特币官方客户端钱包用的Qt，第三方钱包有Python语言开发的，特别是第三方整理的开发库（Api包）很多是Nodejs设计的。比特币的架构，与上面的架构设计基本相同，另外，因为共识算法采用的是工作量证明机制（PoW:Proof of work)，还有一些特殊的挖矿的过程。其他竞争币都是直接来自比特币的分支，所以编程语言相同，具体的技术选型和技术实现上可能有所改进，比如：莱特币，使用了其他的加密算法。

    * 官方网站：[https://bitcoin.org/](https://bitcoin.org/)
    * 源 码 库：[https://github.com/bitcoin](https://bitcoin.org/)
  
 2. Nodejs/Javascript
 
    Nodejs平台强大的网络编程能力，以及js脚本语言的简单快捷，在区块链领域自然少不了它的身影。亿书便是这样一个区块链产品，亿书币是它的协议层，使用了著名的express开发框架，基于http协议开发而成。同时，它采用了授权股权证明机制（DPoS），算法上的改进，让它在处理交易时更加轻量，处理能力大大提升。它提供了强大的协作机制，为数字出版、版权保护提供了便利；扩展了侧链功能，可以基于它开发任何去中心化的应用，从而为专业作者、博客爱好者和开发者提供很多方便。《Nodejs开发加密货币》这本书完整分享了它的源码，从区块链基础概念到代码实现，从基本原理到开发设计思路，都做了比较详细的探索，目前为止，从协议层面深入代码讲解区块链技术实现的书籍极少，这算作一本。
   
    * 官方网站：[http://ebookchain.org/](http://ebookchain.org/)
    * 源 码 库：[https://github.com/Ebookcoin](https://github.com/Ebookcoin)
  
 3. Python
 
    如果是Python语言爱好者，我建议研究研究以太坊（Ethereum）的Python实现。尽管因为The Dao事件闹得沸沸扬扬，但从技术实现的角度来说，仍然值得参考学习。以太坊官方定位为一种开发管理分布式应用的平台，主攻方向就是“智能合约”，并为其定制了一种编程语言Solidity。以太坊的核心是以太坊虚拟机（EVM），允许用户按照自己的意愿创建操作。以太坊给出了Go、Java、Python等多语言的实现。其中以python为基础的实现主要包括三个部分：Pyethapp是客户端部分；pyethereum是核心库，实现了区块链、以太坊模拟机和挖矿等功能；pydevp2p是点对点网络库，实现了节点发现、合约代码传输、加密签名等功能，这三者组合在一起就是完整的区块链实现，后面两个核心库共同组成了协议层。另外，go-ethereum是go语言的完整实现；Ethereum(J) 是纯Java实现，它作为可以嵌入任何Java/Scala项目的库提供。客户端方面，还有Rust、Ruby、Javascript等语言的实现。

    * 官方网站：[https://ethereum.org/](https://ethereum.org/)
    * 源 码 库：[https://github.com/ethereum/pyethapp](https://github.com/ethereum/pyethapp)
  
 4. Go
 
    在多核时代，Go语言备受喜爱，它可以让你用同步方式轻松实现高并发，特别是在分布式系统、网络编程等领域，应用非常广。所以，在区块链开发领域，也有很多使用Go语言的项目。其中，由linux基金会主导的超级账本（HyperLeger），版本库的名字叫Fabric，就是其中一个。该项目试图为新一代的事务应用创建一种开放的分布式账本标准，支持许可式区块链（这种方式可能无法再现比特币那种强大的网络效应）。Fabric的开发环境建立在VirtualBox虚拟机上，部署环境可以自建网络，也可以直接部署在BlueMix上，部署方式可docker化，支持用Go和JavaScript开发智能合约。它采用PBFT分布式算法，网络编程方面用gRPC来做P2P通讯，使用 Protocol Buffer来序列化要传递的数据结构。在架构设计上，Fabric可能与比特币等区块链产品有所不同，但是上述基本组成部分还是不可或缺的。

    * 官方网站：[https://www.hyperledger.org/](https://www.hyperledger.org/)
    * 源 码 库：[https://github.com/hyperledger](https://github.com/hyperledger)
    
    其他编程语言，比如：C#等，也有具体实例，这里就不再列举。总之，针对不同的编程语言，在具体的编码或架构设计上可能有所差别，甚至很大，但是协议层所使用的技术并没有太大的变化。其中，网络编程是重点和难点，多数没有现成的框架可用，都是使用编程语言自身提供的库来设计开发，所以比较底层，非常考验开发者的编码功底。


# 知识图谱

循着上面的分析，我们已经可以了解区块链是什么，并知道怎么实现了，顺便梳理一下其中的编程技术知识，自然也就清晰多了。

 [![区块链知识图谱](/img/blockchain_lib.png "区块链知识图谱")](https://github.com/MinuteBook/blockchain/blob/master/img/blockchain-lib.png?raw=true)

根据个人的理解，我把与区块链相关的知识分为下面5个方面：

 1. 基础知识

区块链是新技术，与之相关的是其背后大量的新概念、新理论。这些知识，虽然不直接体现在编码里，但却是理解区块链，掌握区块链技术的基本知识。所以，理当成为区块链技术不可或缺的一部分。这部分从基本概念入手，到工作原理的描述，就能够把区块链基础知识全部覆盖。

 2. 技术实现

区块链是一项技术，但从上面的分析可以看出，它应该是一种架构应用，架构的实现理当是我们知识库的核心。正如大家看到的，任何一款区块链产品，协议层必须包括点对点网络、加密签名、数据存储、分布式算法等4个部分，应用层也必然要提供钱包、客户端浏览器等基础应用。所以，把这部分独立出来，也是合情合理。

在扩展层的部分，区块链技术可以对接各种应用，比如：金融、物联网、网络安全、版权保护、电子商务等等，现有的很多技术都可以用在这里。只不过，如何与区块链结合，如何实现跨行业使用，自然是这部分内容研究的课题。所以，这里所罗列或涉及到的技术，理应归为技术实现的一个重要部分。

 3. 开发环境

区块链是多项技术的组合，有其自身的复杂性，个别应用对开发环境依赖较大，开发工具与环境搭建，是让开发者快速上手的重要内容。

 4. 项目实践

据说，短短数年，全球区块链产品已经有几千个，其中不乏创新应用。有些优秀的开源产品和项目实践，是最好的学习研究资料。

 5. 开发文档

这个自然不用说了，每一种产品也都会有自己的开发文档。另一个，就是有心的开发者整理汇总的一些资源，可以帮助我们节省很多查询的时间。

我在考虑这个知识体系的过程中，主要思考的是，读者循着这些标签去查阅文章，能否快速掌握区块链技术，并最终上手开发实现一个区块链产品。另外，也刻意规避了与具体编程语言，以及特定领域相关的词汇，唯一可以区分的就是这些节点之下对应的文章标签。所以，这些分类就显得非常中性。也考虑过使用比特币、竞争币、智能合约、数字资产、智能资产等具体领域的实现作为分类方法，但又怕限制了读者的思维，同时随着区块链的发展，这个图谱将不停的修改下去。这里，呼吁一下，希望读到这篇文章的小伙伴提供您的宝贵意见，让我们把这个关于区块链的知识分类图谱做得更加科学合理，使用更加方便。


# 总结
 
这篇文章，我们把区块链技术基础架构描述了一下，需要再次强调的是，这仅仅是一种实现方式，绝非所有的区块链产品都是如此，我们也期待更多创新出现，也相信一定会出现。编程实现罗列了几种编程语言与其实现的典型产品，因为协议层技术较为底层，并没有太多现成的框架需要介绍或讨论，同时，具体的技术细节，也绝非几行字能够罗列清楚，所幸，这些产品都是开源产品，大家可以结合自己的技术背景，进一步查看对应的产品源码，很快就能了解其中的奥妙。

 
作者简介：朱志文，亿书创始人，CSDN区块链知识库特邀编辑。中国区块链俱乐部主创者和发起人，比特币的忠实粉丝，区块链技术的布道者，代表作《Nodejs开发加密货币》。
