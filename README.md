# 地图类型-> 兵力类型人数的映射统计：

关于fs-zj-mountain:
原始兵力，玩家1：9个海军陆战队，9个特种部队；玩家2：12个海军陆战队，1个指挥中心

因此，代码中运行时查询，可以看到 self.enemies 有12个ID是 2022 (marine_rifle_id) 和1个ID是（command_center_id），self.agents 有9个ID是 2022 (marine_rifle_id) 和 9个ID是 2018 (sf_rifle_id)

由于增加或减少兵力，就会使得地图引擎传导至代码侧的unittype 的ID总是变化,具体如下:

例如，如果原地图没有指挥中心的时候，infantry_antitank，sf_rifle，sf_antitank1，sf_antitank2，sf_antiair，marine_rifle，marine_antitank 分别是 2016,2017，2018，...，2022，
增加了 指挥中心后，指挥中心的ID会替代原infantry_antitank的ID ，并变成2016，infantry_antitank的ID会往后偏移一位，即+1，后面的都会+1。

因为，针对这种不确定信，我们通过地图的单位数的人为统计信息，结合代码运行时的ID为XX的数量，准确推理出 某类型单位的ID是什么，根据如此进行映射。

mapname_to_count_mapping.json中存储的是从地图的名字到兵力的映射， 很简单，每个地图对应的列表的第一项是玩家1（也就是AI的兵力数量），第二项是玩家2（脚本兵力数量）
（这个json文件需要人为持续增加地图映射和更新）
（我认为在地图名确定后，兵力就不要变了，你可以复制一个新地图副本并地图名，然后再改兵力类型和数量等配置）

TIPS: 
> 1. 数量为零的兵力类型的设置，不写上去也可以，例如：;
> 2. 即使数量写错了，也不会出现运行错误，但我写了自动报错的逻辑，帮助你看具体的兵力不对齐的错误信息。
