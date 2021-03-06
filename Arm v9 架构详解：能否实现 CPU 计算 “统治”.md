[IT之家](https://www.ithome.com/)4月1日消息 本周三，Arm 发布了最新一代架构 Arm v9，这一架构是在目前已经广泛使用的 Armv8 的基础上，面向未来十年的新一代架构。

![Arm v9 架构详解：能否实现 CPU 计算 “统治”](https://img.ithome.com/newsuploadfiles/2021/4/20210402_084459_294.png)

![Arm v9 架构详解：能否实现 CPU 计算 “统治”](https://img.ithome.com/newsuploadfiles/2021/4/20210402_084459_513.png)

Armv9 架构有三个系列，分别是针对通用计算的 A 系列，实时处理器的 R 系列，微控制器的 M 系列，预计未来两代移动基础设施 CPU 的性能提升将超过 30%。首款基于 Armv9 架构 CPU 的移动处理器最快将在今年底问世，可能来自 MediaTek。

Arm v9 架构的初代版本增强了安全性、机器学习、DSP 性能，Arm v9 架构未来也将持续增强这些性能，并将加入新特性。

最近几年，Arm 架构处理器已经从智能手机为代表的终端向对性能要求更高的 PC、数据中心延伸。从最新的发布可以看到，Arm 希望 Arm v9 架构 CPU 以及基于其 GPU、NPU 处理器能够无处不在。如果 Arm 的目标能够实现，是否可以实现 CPU 计算统治？Arm 的第三个 1000 万出货目标多久能够达成？

## 安全是发挥计算架构潜能最大的挑战

Arm v9 架构的发布会上，安全性被频频提及，与安全相关的技术和介绍的篇幅也很长。Arm 高级副总裁、首席架构师兼技术院士 Richard Grisenthwaite 解释称，“我看来，计算若要充分发挥潜能，安全是最大的挑战，越来越多的私人数据被存放在计算系统中，这让这些数据成为安全攻击的诱人目标。今年网络犯罪损失的金额预估高达 6 万亿美元。”

因此，Armv9 架构在安全性方面做了多方面的工作。首先是引入了 Arm 机密计算架构（Confidential Compute Architecture, CCA），机密计算通过打造基于硬件的安全运行环境来执行计算，保护部分代码和数据，免于被存取或修改，甚至不受特权软件的影响。

![Arm v9 架构详解：能否实现 CPU 计算 “统治”](https://img.ithome.com/newsuploadfiles/2021/4/20210402_084459_607.png)

Arm CCA 将引入动态创建机密领域（Realms）的概念，机密领域面向所有应用，运行在独立于安全或非安全环境之外的环境中，实现保护数据安全的目的。比如，在商业应用中，机密领域可以保护系统中商用机密数据和代码，无论它们正被使用、闲置或正在传输中。

据悉，Arm 会在今年下半年公布 Arm CCA 的更多信息。

内存标签扩展是 Armv9 架构的另一项安全技术。Richard Grisenthwaite 说：“在分析了全球软件报告的大量安全问题后，我们发现许多问题的根源实际上与过去内存安全的老问题有关。这些问题已经困扰计算领域 50 年，两个持续多年特别常见的内存安全问题——缓存溢出和释放后重用。很大一部分的问题是，这些内存安全漏洞被利用之前就能发现问题，这是提高全球软件安全至关重要的一步。”

![Arm v9 架构详解：能否实现 CPU 计算 “统治”](https://img.ithome.com/newsuploadfiles/2021/4/20210402_084459_685.png)

Arm 持续与谷歌合作开发的 “内存标签扩展”技术，可以在软件中查找空间和时间内存安全的问题，允许软件将指向内存的指针与标签建立关联，并在使用指针时检查这个标签是否正确。

Richard 称，内存标签扩展是明年上市的第一代 Armv9 CPU 不可或缺的一部分。支持内存标签扩展的软件也正被引入到安卓 11 系统和 OPENSUSE。

![Arm v9 架构详解：能否实现 CPU 计算 “统治”](https://img.ithome.com/newsuploadfiles/2021/4/20210402_084459_763.png)

Arm 还与剑桥大学在其 CHERI 架构上合作多年，从架构底层来提升安全性。据介绍，CHERI 架构定义了可提供这种封装能力的硬件功能，这在未来将可能促成一个本质上更为安全的计算平台，但这也会使某些系统的变成方式产生重大改变。

不过，这种架构 Arm 已经在和其合作伙伴探索，如果成功，会在未来 5-6 年引入 Armv9 架构，成为 Armv9 架构主要的组件之一。

## 未来两代 Armv9 架构 CPU 性能提升将超过 30%

安全性是计算架构的基础，性能提升则是满足越来越高的计算需求以及多样化计算需求的关键。Arm 预计，新一代架构 Armv9 将保持超过业界 CPU 性能提升的速度，未来两代移动和基础设施 CPU 的性能提升将超过 30%。

![Arm v9 架构详解：能否实现 CPU 计算 “统治”](https://img.ithome.com/newsuploadfiles/2021/4/20210402_084459_857.png)

Richard 强调：“这个数据是根据业界标准评测工具来衡量，30% 的算力提升完全是凭借于本身架构而不是借助于制程工艺来实现。”

计算性能提升非常重要的驱动力就是 AI，Statista Research Department 今年 1 月发布的最近报告估计，到 21 世纪 20 年代中期，全球将有超过 80 亿台搭载 AI 语音辅助的设备。不同设备对于 AI 性能的需求不同，也就需要不同的 AI 处理器。

![Arm v9 架构详解：能否实现 CPU 计算 “统治”](https://img.ithome.com/newsuploadfiles/2021/4/20210402_084459_951.png)

Arm 与富士通合作开发了可伸缩矢量扩展（Scalable Vector Extension, SVE）技术并用在了全球最快的超级计算机 “富岳”上。在 SVE 的基础上，Armv9 中使用了新开发的 SVE2 技术，增强了对在 CPU 上本地运行的 5G 系统、虚拟和增强现实以及 ML 工作负载的处理能力，能够提供实现增强的机器学习和数字信号处理能力。

![Arm v9 架构详解：能否实现 CPU 计算 “统治”](https://img.ithome.com/newsuploadfiles/2021/4/20210402_084500_29.png)

“我们还将通过提升频率、带宽、缓存大小、并减少内存延迟，以最大化 CPU 性能。”Richard 表示。

在解决新问题的过程中，Arm 加入了一些复杂技术，这是否违背了精简指令集（RISC）的初衷？Richard 的观点是：“Arm 架构的精简指令（RISC）核心没有改变，我们依然遵循着注册到注册 (registration to registration) 的操作原则，所以从硬件的角度来看，Arm 指令集仍然保持着精益性。”

Arm 称，除了大幅增强 CPU 内的矩阵乘法，Mali GPU 和 Ethos NPU 也会持续进行 AI 创新，扩展 Arm 的技术能力。

## 统治 CPU 计算

目前，CPU 领域最成功的架构当属 x86，不过 x86 的成功和统治力在于 PC 和高性能计算市场，在 Arm 擅长的智能终端市场并不成功。近几年，Arm 架构在高性能计算领域取得了一些进展，包括上面提到的 “富岳”超级计算机，以及推出采用 Arm 架构的多款服务器。去年，苹果 M1 处理器 Macbook Pro 电脑的推出，也让业界看到了 x86 架构在 PC 市场的统治地位并非牢不可破。

Arm 首席执行官 Simon Segars 说，“Arm 芯片实现 1000 亿颗的出货花了 26 年，如果预测准确，接下来一年，我们的合作伙伴出货的 Arm 芯片将累计达到 2000 亿颗。也就是说，我们的第二个 1000 亿的出货将在短短 5 年内达成。”

目前 Arm 架构的芯片出货已经超过 1800 亿颗，Armv9 架构会成为实现 Arm 芯片 3000 亿颗芯片出货的先驱。没有人能准确预估 Arm 实现第三个 1000 亿颗芯片出货的时间，但可以明确的是 Arm 希望其芯片能够为所有智能计算提供算力，也就是让其芯片在未来无处不在。

为了实现这个目标，同时满足行业从通用计算向普遍的专用处理发展的需求，Arm 也开始强调全面计算的理念。全面计算设计方法包含 Arm 的 CPU、GPU、NPU，通过将全面计算的设计原则应用在包含汽车、客户端、基础设施和物联网解决方案的整个 IP 组合中。

![Arm v9 架构详解：能否实现 CPU 计算 “统治”](https://img.ithome.com/newsuploadfiles/2021/4/20210402_084500_125.png)

与此配合，Arm 也需要在标准化程度上取得平衡。Richard 说：“如果过多的标准化，那么合作伙伴将无法开发合适的专用解决方案。而如果太少的标准化，我们得承担低价值、形同实异的解决方案的风险。这将让软件生态系统的成本增加、且毫无益处。”

Arm 在服务器领域中已经看到了标准化平衡的价值，推出了 “服务器基础架构 SBSA”和相关的认证计划 “服务器就绪”。

![Arm v9 架构详解：能否实现 CPU 计算 “统治”](https://img.ithome.com/newsuploadfiles/2021/4/20210402_084500_248.png)

“我们也正在扩大标准化的范围，Arm SystemReady 将服务器就绪计划的概念从云端延伸到物联网边缘等广泛的设备上，以实现通用操作系统及虚拟机管理程序之间的交互运作。”Richard 说。

![Arm v9 架构详解：能否实现 CPU 计算 “统治”](https://img.ithome.com/newsuploadfiles/2021/4/20210402_084500_341.png)

![Arm v9 架构详解：能否实现 CPU 计算 “统治”](https://img.ithome.com/newsuploadfiles/2021/4/20210402_084500_451.png)

如果 Arm 的全面计算以及标准化探索成功，从终端到边缘再到云端，Arm 是否就能够实现在未来的计算统治？实现 3000 亿颗甚至更多芯片出货又会有多快呢？

## 小结

现在看来，有两大方面的阻碍，一方面是在复杂的国际形势下，同属精简指令集的 RISC-V 正在快速发展，加上 x86 阵营 intel 和 AMD 也在加强 x86 的竞争力，Arm 要真正撼动 x86 的优势领域并非易事。

另一方面，中国作为芯片进口的大国，Arm 与 Nvidia 的收购交易，以及美国对中国领先芯片设计公司的出口限制，让客户产生担忧。

对于 Armv9 是否以供给包括华为在内的中国企业的问题，Arm 的官方回复是：“Arm 既有源于美国的 IP，也有非源于美国的 IP。经过全面的审查，Arm 确定其 Armv9 架构不受美国出口管理条例 (EAR)的约束。Arm 已将此通知美国政府相关部门，我们将继续遵守美国商务部针对华为及其附属公司海思的指导方针。”
