# 地图类型-> 兵力类型人数的映射统计：

关于fs-zj-mountain:
原始兵力，玩家1：9个海军陆战队，9个特种部队；玩家2：12个海军陆战队，1个指挥中心

因此，代码中运行时查询，可以看到 self.enemies 有12个ID是 2022 (marine_rifle_id) 和1个ID是（command_center_id），self.agents 有9个ID是 2022 (marine_rifle_id) 和 9个ID是 2018 (sf_rifle_id)

由于增加或减少兵力，就会使得地图引擎传导至代码侧的unittype 的ID总是变化,具体如下:

例如，如果原地图没有指挥中心的时候，infantry_antitank，sf_rifle，sf_antitank1，sf_antitank2，sf_antiair，marine_rifle，marine_antitank 分别是 2016,2017，2018，...，2022，
增加了 指挥中心后，指挥中心的ID会替代原infantry_antitank的ID ，并变成2016，infantry_antitank的ID会往后偏移一位，即+1，后面的都会+1。

因为，针对这种不确定信，我们通过地图的单位数的人为统计信息，结合代码运行时的ID为XX的数量，准确推理出 某类型单位的ID是什么，根据如此进行映射。

json中未来将存储
