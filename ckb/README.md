## 介绍
Nervos CKB is a public permissionless blockchain, the common knowledge layer of Nervos network.

## image

nervos/ckb:v0.117.0

## dockerfile

https://github.com/nervosnetwork/ckb/blob/master/docker/hub/Dockerfile


## exec

docker run -it --rm --entrypoint=bash nervos/ckb:v0.117.0

## 参数


## 暴露端口

* 8114 -- RPC
* 8115 -- P2P


## 获取信息

```
$ export API_URL=http://127.0.0.1:30004
$ ckb-cli rpc get_tip_block_number
13960867

$ ckb-cli rpc sync_state
assume_valid_target: 0x84ef5fe7cbf4242bdcac76326aa33f15b9cc41958e9d891157b8a6066dad0f31
assume_valid_target_reached: true
best_known_block_number: 13995851
best_known_block_timestamp: "1725966683263 (2024-09-10 11:11:23.263 +00:00)"
fast_time: 3255
ibd: true
inflight_blocks_count: 459
low_time: 7835
min_chain_work: 0x3314412053c82802a7
min_chain_work_reached: true
normal_time: 5464
orphan_blocks_count: 410
orphan_blocks_size: 947181

$ ckb-cli rpc local_node_info
active: true
addresses:
  - address: /ip4/0.0.0.0/tcp/8115
    score: 1
connections: 8
node_id: QmWefN8AHJK7uZ3iSTzRNRGcw25wXFtqPz5wAGvuoi6DMP
protocols:
  - id: 100
    name: /ckb/syn
    support_versions:
      - "2"
      - "3"
  - id: 103
    name: /ckb/relay3
    support_versions:
      - "2"
      - "3"
      
      
$ ckb-cli rpc get_blockchain_info
alerts: []
chain: ckb
difficulty: 0x3eda3cfdef27bacf
epoch: 1236969019418909
is_initial_block_download: false
median_time: "1725874633649 (2024-09-09 09:37:13.649 +00:00)"

$ kubectl exec -it -n default ckb-0 -c ckb -- du -s /var/lib/ckb
58111284        /var/lib/ckb
```
