---
title: ECS 2021 exam paper
date: 2022-11-27 16:27:42
tags:
---

### 1.

*马克-迪恩是一家成立于1876年的百货公司，在英国各地拥有多家实体店。该百货公司已决定将其销售从实体店过渡到网上商店。几十年来，该组织==在基础设施方面进行了大量投资==，但决定向云计算基础设施过渡。 该组织向云计算过渡的动机有很多，包括人员的变化。多年来，==该组织失去了许多==内部的软件工程师和技术人员。该组织仍有一个由技术和专家组成的小团队，==可以管理端点、访问管理和数据治理==。然而，该组织在管理和配置应用程序、网络控制、操作系统或==一般基础设施==方面==没有足够的专家人员==。管理团队也承认，作为过渡的一部分，它可能不得不从现有的软件解决方案过渡到==外部供应商提供的==更现代的软件产品。*

*组织的管理团队知道有不同的云计算服务模式，但不确定哪种服务模式对组织来说是最佳的。*

#### 论证该组织在特定情况下的最佳服务模式。 (约200字)

<u>结论：使用社区云模式</u>

###### <u>理由：</u>

<u>1.从基础设施提供的受众角度来看，百货公司面向的群体不是私有企业或单位内部，因此不用私有模式，而百货公司也不属于公共机构，因此不适用公共部署模式，百货公司的基础设施面向的的受众是有购物需求的人群，</u>

<u>2.从基础设施管理角度来看，此公司在前期对基础设施有大量投资，因此不需要云计算提供方提供额外基础设施，且公司内部虽有可以管理断电的专业人员，然而缺少管理和配置应用程序、网络控制、操作系统或一般基础设施的专业人员，因此需要由第三方和内部人员共同管理基础设施</u>

<u>3.管理层同意公司需要从外部提供上哪里获取更现代的软件产品</u>

*管理团队认为，利用外部供应商的云计算的许多好处是由多个租户使用相同的基础设施实现的。然而，管理团队担心任何外部供应商将如何确保对数据的严格访问控制，任何外部供应商如何防止数据在传输和静止时泄漏，以及外部供应商将数据与其他租户的数据一起存储。*

#### ==论证三个能够解决这些问题的解决方案。 (约200字)==

哪些问题？

再多用户公用的情况下，确保对数据的严格访问控制，防止数据泄漏，将数据一起存储

<u>1.针对严格访问控制：明确数据所有权，只有持有相应所有权的用户可以访问自身数据，</u>

<u>使用hypervisor虚拟机管理系统来进行软件隔离</u>

<u>2.针对防止数据泄露：采取数据加密和数据隔离，并使用恰当的基础设施架构以确保不同用户之间的数据在传输和静止时不会产生混合。</u>

<u>3.针对数据一起存储的问题，由于数据混合存储是不可避免的，所以云服务供应商应使用数据消毒的方法来对混合存储的数据进行处理，可以使用数据备份以随时进行数据恢复</u>



*该公司有一个老化的主机系统，对变化有抵触。合规小组指出，该组织需要将数据加密到一个特定的标准。技术团队建议，这个特定的标准对于现有的主机系统来说==要求太高==。该小组建议，进化系统需要大量的投资，需要36到48个月。 合规小组指出，特定标准==必须在18个月内应用==。*

#### 论证在给定环境下加密数据的最佳方案。

关键词：加密，少改变已有系统，能快速实施

<u>可以使用BITW来加密数据</u>

<u>理由：</u>

<u>1.BITW的工作方式是插入到现有的系统中，而无需更改通信端点，所以无需对老旧的系统进行改变，这符合此系统对变化抵触的现状</u>

<u>2.BITW允许系统输出未加密的数据，相当于一个黑箱系统，这对于当前主机系统由于低配置而无法实现过高的数据加密标准的现状是使用的</u>

<u>3.相较于从内部进行加密或更改，使用BITW所花费的时间更少，适用于当前compliance team提出的时间限制</u>

### 2.

*Inmos International是一家技术集团，为世界各地的企业提供电话会议服务。该公司是一次攻击的受害者，这次攻击导致了计划外的停工，公司所依赖的654台虚拟机被摧毁。虚拟机的丢失导致超过16000名客户无法访问他们的账户和数据。 管理团队怀疑这次攻击是来自内部的一个或多个雇员。管理团队已经要求Holberton, Antonelli和Meltzer进行调查，以确定疑似网络攻击的结构，并提出适当的防御措施。 霍伯顿、安东内利和梅尔策已经审计了系统并审查了日志，以确定过去48周的相关安全事件。以下事件被认为是相关的。*

*已经恢复了定制的源代码，这是破坏虚拟机的核心。这些定制的源代码显示了对基础设施和系统的深入了解，以及提前的组织信息。*

*虚拟机上有789个文件，一些员工的访问率异常高，访问时间异常长，没有明确的理由。*

*37个文件的文件名具有误导性，这些文件被伪装成媒体文件，而实际上是在员工工作区账户中发现的敏感PDF文件。*

*已发现1098封不同员工之间的电子邮件，讨论规避公司系统的技术控制，以安装第三方商业软件，如媒体播放器、照片浏览器和视频游戏。*

*在整个组织的678个员工系统中，记录应用程序使用情况和监控员工使用系统的技术控制已经被禁用。*

 *在整个组织的546个员工系统中发现了未经授权的第三方软件，该软件允许个人将其智能手机作为外部硬盘来传输文件。*

*Holberton、Antonelli和Meltzer一致认为，仅靠这些事件还不足以==确定攻击的解剖结构和确定适当的防御措施==。三人需要使用一种方法来确定网络攻击的剖析和计划防御。*

*Holberton、Antonelli和Meltzer提议使用一种方法来更好地理解网络攻击，但不能就最佳方法达成一致。 霍伯顿认为STRIDE将是最佳方法，安东内利建议CAPEC将是模拟和确定攻击的最佳方法，而梅尔策认为网络杀伤链方法将是最佳方法。*

#### 评估Holberton、Antonelli和Meltzer在特定情况下提出的每种方法。论证给定背景下的最佳方法。 (约400字)

<u>最佳方法肯定是kill chain啦，只有killchain最适合于解析攻击和制定防御</u>

<u>H提出的STIDE：</u>

<u>STIDE方法的设计目的主要是让软件开发人员考虑常见的威胁并为软件开发过程中的安全提供支持，且由于STRIDE主要用于感知威胁而不是发现具体威胁，所以对于当前确定具体威胁和攻击的目标，STRID不是最佳方法</u>

<u>A提出的CAPEC：</u>

<u>使用CAPEC的主要动机是为了更好的了解攻击发起者，在分析时重点关注的是对方的观点，而CAPEC的功能则和STIDE一样，主要是为软件开发过程中的安全提供支持，这不符合当前形势。根据文中案例，当前需求是理解网络攻击以及制定适当防御措施，而CAPEC由于没有对攻击方式进行优先级排序，所以针对确定最佳攻击方法这一目标价值不大因此不应该使用CAPEC</u>

<u>M提出的KillChain：</u>

<u>Killchain支持组织或个人对网络攻击进行结构解析并指定防御措施，这符合当前的需求，且KillChain对于入侵行为来说是最优方案，所以应使用killchain</u>



*霍伯顿、安东内利和梅尔策需要确定网络攻击的结构。三人确信，网络攻击来自于==内部人员==，即公司内部的一个受信任的人。*

#### 使用(a)中确定的最佳方法，在给定的背景下制定攻击的剖析。论证对该方法的任何修改或调整 (约450字)

重点：内部人员

<u>将killchain修改成针对内部人员的killchain</u>

<u>攻击剖析：</u>

<u>将攻击分解为以下五个阶段：</u>

<u>侦察，漏洞利用Exploitation，准备，混淆和渗透</u>

<u>侦查阶段：部分员工对虚拟机中文件的异常高频率访问可能是在对企业内部有价值的信息或资产进行侦察</u>

<u>攻击者在虚拟机中植入了定制的源代码，这些源代码显示了对内部基础设施的深入了解，很明显这是在侦查阶段对公司内部系统所进行的调查</u>

<u>利用阶段：员工使用电子邮件来讨论如何规避公司系统的技术控制属于利用漏洞阶段，这一阶段其目标是利用系统的安全弱点或规避安全措施</u>

<u>准备阶段：员工在工作区存储有诱导性的PDF文件行为属于killchain中的准备阶段，在这一阶段员工试图把想要从公司中窃取的信息或资产提前伪装。</u>

<u>混淆阶段：攻击者提前禁用了员工监控系统和app使用历史记录系统，这属于killchain的混淆阶段，目的是掩盖自身的攻击行为。</u>

<u>渗出阶段：攻击者在系统中安装未授权且允许使用智能手机来向外传输问价的的第三方软件，这一行动属于渗出阶段，目的是从组织内部将窃取到的信息或资产转移出去</u>

<u>方法调整：</u>

<u>根据题意，三人已经确信攻击是来自内部人员，因此不应使用原始的kill chain而是用改进后的Insider Cyber Kill Chain Model，具体调整：</u>

<u>1.由于攻击者来自内部，因此应跳过kill chain中的Weaponisation，Delivery，Installation和Command and Control以及Actions on Objectives分析阶段，取而代之的是漏洞利用Exploitation，准备，混淆和渗透，因为前者是针对来自外部人员的攻击行为进行分析，而后者则针对内部人员。</u>



*管理团队希望确保公司在未来不容易受到这种攻击*。

#### 论证三种不同的能以最佳方式防御(b)中确定的攻击的防御步骤，在什么阶段应该采取这些步骤，为什么在该阶段采取这些步骤。 (约450字)

<u>Detect:识别探索网络或访问系统的攻击者</u>

<u>这一方式适用于侦察，混淆和利用阶段，对于侦查阶段中部分员工的高频率访问可以大概识别出供给者名单，在混淆阶段对于提前禁用相关系统的人员进行识别也可以发现攻击者。</u>

<u>在利用阶段，对于使用邮件进行讨论的员工的记录也是对攻击者进行识别的一种办法。</u>

<u>Deny：  针对试图获取资源和干扰数据的行为</u>  

<u>这一方式适用于准备阶段，侦查阶段和渗出阶段，对于准备阶段攻击者试图存储诱导性文件的这一行为可以进行拒绝，对于侦查阶段攻击者试图植入恶意的定制源代码的行为也可以进行拒绝，对于渗出阶段攻击者安装未授权软件的行为也可以进行拒绝</u>

<u>Disrupt：   针对任何试图改变向外传输或向组织外传输数据的行为，如果被认为是一种担忧的话</u>  

<u>这一方式适用于渗出阶段，在攻击者试图通过智能手机转移内部信息时可以对将被转移的信息进行加密或者破坏</u>

### 3.

*Granville & Clay Services向整个欧洲的卫生机构提供专门的医疗记录备份服务。医疗记录主要包括为病人生成的标准表格和信件，其中==只有特定的变量发生变化==，如每个病人的姓名、出生日期和病人说明。 管理团队希望提高基础设施的==利用率==，以实现利润最大化和浪费最小化。管理团队希望在现有的基础设施上==存储更多的数据==，他们希望确保客户的==无缝过渡==，不要求下载特殊的软件。*

####  设计并论证一个适当的解决方案，以减少给定环境中的冗余数据。 (约300字)

<u>根据题意，医疗记录的存储形式主要是内容格式类似的表格和信件，文件模式非常类似但却有细微不同，因此可以使用单向哈希值来对医疗记录的二进制数据进行指纹识别，如果新加入的医疗记录的哈希值在数据库中有相同记录，则不把新的医疗记录的二进制添加进来，而是将其指向已有的相同数据，反之如果新的医疗记录哈希值从未在数据库中出现过，则将其二进制数据添加并存储。使用这样的方法可以减少重复的医疗数据，提高基础设施的利用率。</u>

<u>其次，整个冗余数据清除过程应该是基于目标的，文中提到管理团队希望确保用户能做到无缝过渡，因此不能使用基于源的数据删除，因为此方式需要客户的客户端来协同工作，甚至可能要求客户更新软件或者下载特殊软件，这显然与题意不符，因此整个冗余数据删除过程只能在存储数据的服务端进行，即在服务器中对冗余数据进行检索和删除</u>

*管理团队关注任何建议的解决方案的安全性，并希望所有的医疗记录都被加密。管理团队还对恶意员工的威胁以及他们如何破坏该方法表示关切。*

#### 完善(a)中提出的解决方案，以便在给定的环境中纳入加密功能。论证所采取的任何设计决定，并讨论概率性和确定性加密方案之间的区别以及在特定情况下的意义。 (约450字)

<u>在a中我们决定使用fingerprint来减少信息冗余，这种方式可能有以下隐患：</u>

<u>1.医疗记录存储了患者的隐私信息，攻击者可以通过生成特定的记录来判断其感兴趣的患者信息是否在医疗记录的信息库里，以达到某种针对特定个人的目的。由于医疗记录形式的特殊性，即每封医疗信件的差异都是极微小的，因此居心叵测者可能会暴力生成形式相同的信件来尝试知晓特定信息的存在</u>

<u>2.除确认特定信息是否存在以外，攻击者也可能会直接窃取特定的医疗信息。</u>

<u>3.此外，由于持有fingerprint就能得到特定文件的特性，攻击者也有可能通过窃取fingerprint的方式来对文件进行入侵。</u>

<u>针对隐患1，我们应该采取数据混淆的方式，来掩盖真实的数据，防止攻击者通过恶意的荣誉删除操作来达到识别特定信息存在性的目的</u>

<u>针对隐患2，我们可以采取加密的方式，将医疗记录的二进制文件转换成加密后的密文形式，确保在传输和精致时不会被非用户进行攻击，有效防止攻击者窃取数据</u>

<u>针对隐患3，我们应该我们应该使用POW方法，来确认用户是否是医疗记录的所有人，以防止指纹被窃取或者被滥用以达到攻击目的。</u>

<u>概率性加密会在加密过程中加入随机性，使得即使有相同的输入，产生的输出也会不同，</u>

<u>而确定性加密则确保了输入形同输出一定相同</u>

<u>在当前案例的情况下，概率性加密能确保医疗记录不会被暴力生成以达到确认特定信息的存在的目的，使得攻击者不能轻易确定原始数据，但是在清除冗余数据时的效率会大大降低，而确定性加密虽然对清楚冗余数据是友好的，但是安全性不如概率性加密</u>



*管理团队关注的是，任何拟议的利用加密的解决方案可能会影响其遵守一些病人的个人权利的能力，特别是被遗忘的权利。管理团队特别关注个人要求删除其数据的权利。*

#### 论证(b)中提议的解决方案是否与被遗忘的权利相冲突。如有必要，概述对(b)中解决方案的任何进一步改进。 (约300字)

看不懂题
