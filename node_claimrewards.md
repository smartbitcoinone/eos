# 节点奖励规则

1. SBC发行总量是100亿。
1. 每年奖励发行总量的1%。
2. 每0.5秒产一个块儿，每天生成的节点块儿数是`2*24*3600`， 每年生成的块儿数是`52*7*24*2*3600`
3. 最快每天领取一次奖励。

## 1%增发分配策略
1. 增发的25%的奖励放在产快奖励池中。
2. 增发的75%的奖励放在投票奖励池中。

## bp领取规则
1. bp产块的收益规则：

	```
	producer_per_block_pay = (gstate.perblock_bucket * prod.unpaid_blocks) / gstate.total_unpaid_blocks
	bp产快收益 = 产快收益池 * bp未获取收益的产块儿数 / 所有bp未获取收益的产块儿数
	```
2. bp投票收益规则：
	```
	prod_vote_pay = (g.vote_bucket*p.total_votes) / g.total_produver_vote_weight
	bp投票收益 = (总的投票奖励池 * 该bp总的投票数) / 总的bp投票权重 
	```
