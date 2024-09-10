## 介绍
Bitcoin Core is an open source project which maintains and releases Bitcoin client software called “Bitcoin Core”.

## image

lncm/bitcoind:v27.0

## dockerfile

https://github.com/lncm/docker-bitcoind/blob/master/27.0/Dockerfile

## exec

docker run -it --rm --entrypoint sh registry.devops.rivtower.com/sparkos/bitcoind:v27.0

## 参数

默认连主网，  -testnet 连测试网

为了连接闪电网络节点，ZeroMQ notification 需要打开， -zmqpubrawblock=tcp://0.0.0.0:28332", "-zmqpubrawtx=tcp://0.0.0.0:28333

-prune 550  Automatically deletes previous block files to stay below this target size. 最少550MB，可以裁剪存储，减少磁盘占用

如果要连接tor代理，需要增加 -proxy 参数，参见 https://github.com/bitcoin/bitcoin/blob/master/doc/tor.md  请访问 https://bitnodes.io/，使用 “check node” 工具，确保你的节点可以接受连接。
## 暴露端口

* 8080  -- rest
* 8333 18333 18444 -- P2P network (mainnet, testnet & regnet respectively)
* 8332 18332 18443 -- RPC interface (mainnet, testnet & regnet respectively)
* 28332 28333 -- ZMQ ports (for transactions & blocks respectively)

## 获取信息

```
$ kubectl --kubeconfig ~/.kube/config exec -n testnet bitcoin-0 -c bitcoin -- bitcoin-cli getchainstates
{
  "headers": 858600,
  "chainstates": [
    {
      "blocks": 858600,
      "bestblockhash": "00000000000000000000d53f8ca46e86625f05a074d70f47013914d308342dd1",
      "difficulty": 86871474313761.95,
      "verificationprogress": 0.9999862022721966,
      "coins_db_cache_bytes": 8388608,
      "coins_tip_cache_bytes": 461373440,
      "validated": true
    }
  ]
}

$ kubectl --kubeconfig ~/.kube/config exec -n testnet bitcoin-0 -c bitcoin -- bitcoin-cli getnetworkinfo
{
  "version": 270000,
  "subversion": "/Satoshi:27.0.0/",
  "protocolversion": 70016,
  "localservices": "0000000000000c08",
  "localservicesnames": [
    "WITNESS",
    "NETWORK_LIMITED",
    "P2P_V2"
  ],
  "localrelay": true,
  "timeoffset": -1,
  "networkactive": true,
  "connections": 0,
  "connections_in": 0,
  "connections_out": 0,
  "networks": [
    {
      "name": "ipv4",
      "limited": false,
      "reachable": true,
      "proxy": "127.0.0.1:9050",
      "proxy_randomize_credentials": true
    },
    {
      "name": "ipv6",
      "limited": false,
      "reachable": true,
      "proxy": "127.0.0.1:9050",
      "proxy_randomize_credentials": true
    },
    {
      "name": "onion",
      "limited": false,
      "reachable": true,
      "proxy": "127.0.0.1:9050",
      "proxy_randomize_credentials": true
    },
    {
      "name": "i2p",
      "limited": true,
      "reachable": false,
      "proxy": "",
      "proxy_randomize_credentials": false
    },
    {
      "name": "cjdns",
      "limited": true,
      "reachable": false,
      "proxy": "127.0.0.1:9050",
      "proxy_randomize_credentials": true
    }
  ],
  "relayfee": 0.00001000,
  "incrementalfee": 0.00001000,
  "localaddresses": [
    {
      "address": "bgsn7qhhi6ovuq7jc5z62oq4kyvewzrpfatctafateq4gvqyyl7phgid.onion",
      "port": 8333,
      "score": 4
    }
  ],
  "warnings": ""
}
```