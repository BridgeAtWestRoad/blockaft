# blockaft
an amazing game on chain



## 简介
一个纯2D平面的游戏。在一个比较巨大的2D空间中，玩家寻找矿块并采矿，获得资源。这其中可能获得的资源包括2类：一类是游戏资源，一类是奖励本身(kaft)。每轮周期之后，会根据奖励的比例，分配整个奖金池里面的奖金。游戏设计受到minecraft, factorio的启发。

## 游戏空间

### 空间的大小
考虑一个1万x1万格的2D空间，如果每个格子用一个字节表示，这将消耗100MB来存储。不清楚这个量级对于EOS来说是否轻松。可以考虑各种优化方案，例如压缩或者随机种子等。

这整个空间构成游戏的地图。如果不采取特别的方法，所有玩家从始至终就知道整个地图的所有细节。需要找到合适的办法才能把地图状态保存为私密数据，只向玩家们分别发送他们附近的地图状态。

### 行走速度
玩家在游戏中按一定速度行走，例如每0.5秒走一个格子。这个速度大致是一个RPG游戏中的正常行走速度，而且0.5秒正好也是eos出块的周期。按这个速度，玩家走完地图的一个边需要花费5000秒，也就是1小时23分钟多一点。

可以考虑有更快的行走方式。例如，如果在游戏中获得马匹。或者制作车辆、铁路。

### 地形
简单起见，地形的分类大致如此：
- 平地：平地可能有不同的外貌，但本质是一样的：可以畅通无阻。
    - 泥土
    - 沙地
    - 草地
- 资源块：实际上是在平地的基础之上附加了资源。资源可以有不同用处。在被采完之前，它们都会阻挡通行。资源被采完之后，露出本身的平地，变成畅通。
    - 矿：采集得到游戏奖励（kaft）本身，还可能会爆出一些特别的道具
    - 树木：采集得到木材
    - 石头：采集得到石头+金属

### 制作
玩家可以使用收集的游戏资源制作物品。物品的主要最终目的大致是加快采集效率、行走效率、运输能力等。

### 采集
不同类型资源的采集难度不同，同种资源的采集难度相同。采集时间由采集效率和采集难度决定。例如，玩家的基础效率为1，一个难度为120的资源，需要花费120个基本时间单位。每个时间单位是0.5秒，正好是1个eos出块周期。采集需要花费1分钟。

在采集的过程中，实际上发生的是每一个周期内都会记录下这个周期内采集者的“贡献”（等于玩家的采集效率）并从资源身上减去相应的耐久度。当资源的耐久减为0那一刻，此时分为2种情况。如果是游戏资源，则此时位于资源周围格子的所有玩家（一共8个格子）都会被平均分配到相应的资源（对于不够分的情况，有些人就会得到少一些，按一定规则）。如果是奖励资源，则自动根据贡献的百分比分配，无论此时玩家位于哪里。对于奖励资源中的道具，则是按贡献的比例作为获取的概率。


