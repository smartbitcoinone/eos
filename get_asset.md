# 通过构造离线交易来领取SBC步骤
1. 下载[ONE钱包](http://app.onechain.one/appstart.html).
2. 在ONE钱包中创建SBC账号.
3. 使用EOS的私钥来签名并构造离线交易, 然后PUSH. 完成从快照账户到新SBC账号中的转账.

## 构造离线交易

NOTE:
   1. 可以使用EOS的cleos程序。 
   2. 需要解锁钱包！！！
   3. --url SBC Full Node 地址(SBC的Full Node) "http://node001.bitpq.com:18000”
   
SBC Full Node

address | http port | p2p port
---- | --- | ---
node001.bitpq.com | 18000 | 19000
node002.bitpq.com | 18000 | 19000
node003.bitpq.com | 18000 | 19000
node004.bitpq.com | 18000 | 19000
node005.coinpp.com | 18000 | 19000
node006.coinpp.com | 18000 | 19000
node007.coinpp.com | 18000 | 19000


```
/alidata/appserver/eos/build/programs/cleos/cleos --url http://node001.bitpq.com:18000 --wallet-url http:
//localhost:6666 transfer <your-account> <receive-account> "0.1 SBC" "" -d -j -x 900
```

## push 交易

```
/alidata/appserver/eos/build/programs/cleos/cleos --url http://node001.bitpq.com:18000 --wallet-url http://localhost:6666 push transaction ./tx.json
```


### tx.json文件示例

```
{
  "expiration": "2018-07-18T09:10:52",
  "ref_block_num": 48325,
  "ref_block_prefix": 3658920525,
  "max_net_usage_words": 0,
  "max_cpu_usage_ms": 0,
  "delay_sec": 0,
  "context_free_actions": [],
  "actions": [{
      "account": "eosio.token",
      "name": "transfer",
      "authorization": [{
          "actor": "zhangzhichao",
          "permission": "active"
        }
      ],
      "data": "10420821d0186935404d43ae7d364dfb6400000000000000045342430000000000"
    }
  ],
  "transaction_extensions": [],
  "signatures": [
    "SIG_K1_JzRBUtj9mNgPNdM81YK29Jgm93AMRYT2RwFq8UN5WwBpfEfFw9Ky5tagDcBJCj14jWyW4i6aN62AUMdJiGjnewAz4XCNFU"
  ],
  "context_free_data": []
}

```
