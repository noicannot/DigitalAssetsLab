# 什么是定序器
定序器在许多**rollup**系统中都属于享有特权的参与者。它们接收来自用户的交易，对其进行排序并批量提交到**Layer1**（第一层）上。
定序器之所以存在，主要是因为单一协调者简单高效。现阶段，每个rollup系统通常都会有一个定序器，由系统创建者运行。

定序器负责为交易排序。因此，在收到用户的交易后，定序器可以立即将其挖出，并向用户返回确认。这极大地改善了用户体验。定序器会攫取**MEV**(矿工获取的回报)。
如果定序器忠于职守，则一切都好。但是，**如果定序器作恶，欺骗用户并试图破坏网络，我们该怎么办？最重要的问题是：定序器可以偷用户的资金吗？**
不能。状态转换的有效性由rollup 架构保障（Optimistic Rollup 靠的是欺诈证明，zk-Rollup 靠的是有效性证明）。
**定序器能审查用户的交易吗？**
没错，它确实可以。**定序器通常是JSON RPC 节点** （是一种无状态,轻量级的远程过程调用）。与 Infura 类似，定序器甚至可以谎报网络状态或审查用户交易。幸运的是，审查不是什么大问题，因为所有 rollup 系统都可以通过不可审查的 Layer1 来发布 Layer2 交易。协议会强迫定序器在几分钟内将用户交易打包到 rollup 内。　　
如果定序器谎报状态，用户需要自己运行节点，根据发布到 Layer 1 的批量交易重新创建 rollup 状态。
最后，定序器可以谎称交易已得到即时确认吗？
可以。定序器可以谎报当前网络状态以及用户交易是否被打包。　　
例如，定序器可以对用户谎称交易已成功，但是实际上被撤销了。用户只有基于 Layer1 重新创建 rollup 状态之后才会发现自己被骗了。只有被发布在 Layer1 上，rollup 交易才算是被敲定了。这就是为什么 Rollup 的 Web 3.0 库一般可以让开发者轻松构建用户界面，以告知用户 Rollup 交易的处理进度。　　

未来有可能采取的一种解决方案是，让定序器在收到用户交易时签名确认，如果交易没有被打包到rollup，用户可以惩罚定序器。这可以通过瞭望塔之类的服务自动化执行。　
定序器技术还处于发展初期。未来，我们将看到更多复杂的设计来解决我提到的很多问题。我们也可以运行一个由定序器组成的免许可型 PoS 网络来代替单个许可型定序器。每一批交易都由网络中随机选取的定序器打包到 Layer1 上。这会大幅增强抗逆性和抗审查性。当然了，每个定序器都需要提供保证金，一旦作恶就会遭到罚没。其它项目如 Arbitrum 在试验一种公平的协议来发现正确的交易排序。当然，也可以不打击 MEV，而是拥抱 MEV：参与方通过竞标的方式来获得在一段时间内运行定序器的权利（但是这个想法存在一些问题）。总之，IMO（
In my opinion的缩写，意思是在我看来）定序器在去中心化和速度之间取得了良好的平衡。


 ## rollup
 rollup 顾名思义，就是把一堆交易卷（rollup）起来变成一个rollup交易，所有节点接收到这个rollup交易之后，不去执行被卷起来的逻辑，而只去接收这些逻辑的执行结果。因此这个rollup交易所需要的gas会远小于执行这些交易的gas。
 关于这种把交易卷起来的方法，一个区块中就能装下更多的交易了，而TPS(事务处理系统)也就上去了。
 这些卷起来的交易和这些交易之后变更的状态（比如账户信息）都会被挪到链下的一个账本上，这个账本由一些专门的节点负责验证和维护 ，并定期将这个账本的状态做个摘要发到以太坊上。
 以太坊里会有一些专门的节点负责去给所有交易做计算，然后，把 这些交易打包起来生成一个摘要，告诉所有节点“这些是我们算完之后给你总结出来的结论，你们照着做就是了。”
 rollup主要分成optimistic rollup 和 zk-rollup，两者在rollup的方法和原理上都十分不同。
 #### Optimistic Rollup
 Optimistic Rollup（OR）：
 * 以太坊：所有交易和状态都记录在链上。
 * Plasma：所有交易和状态都记录在链下。
 * OR：所有交易和一批交易处理之后的最终状态的摘要记录在链上，但交易的计算和具体状态变更放在链下进行。

 这叫什么扩容呢？
 以太坊现在最大的瓶颈是gas，而OR省了gas。
 #### Zk-rollup
 zk指的是zero knowledge（零知识），这种rollup方案基于一个叫做“零知识证明”的密码学工具。
 在ZR中，链上保留交易以及一批交易之后，所有状态的变化的摘要。


ZR采用的是“有效证明（Validity proof）”的逻辑而OR采用的是“作恶证明（Fraud proof）”的逻辑，即：
* 在OR中，有一个或者几个验证者，他们通过签名的方式担保“状态A在经过这些交易TX之后会变成状态B，我验证了”。然后，在一段时间的挑战期（通常是一周或者两周）之内，如果有人提出“你担保的结果和实际交易执行的结果不符”并提供证据，那么，错误的结果将会被回滚，挑战者可以获得担保人在链上抵押的一部分押金。
* 在ZR中，验证节点在链下通过零知识证明算法，生成一个证明P并与状态A，B与交易TX一起上传上链，相当于是表示“状态A在经过这些交易TX之后会变成状态B，你可以通过验证P来证实这一点”。在ZR中，不需要挑战期，因为密码学可以保证验算P就等价于验证了状态B是经由交易TX得出的。
