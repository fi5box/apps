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
13987245

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
```
