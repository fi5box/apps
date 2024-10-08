## 介绍
Lightning Network Daemon ⚡️

## image

lightninglabs/lndinit:v0.1.22-beta-lnd-v0.18.3-beta.rc1
lncm/tor:0.4.7.13

## dockerfile

https://github.com/lightninglabs/lndinit/blob/main/Dockerfile
https://github.com/lightningnetwork/lnd/blob/master/Dockerfile

## exec

docker run -it --rm --entrypoint bash registry.devops.rivtower.com/sparkos/lnd:v0.18.2-beta

## 参数

tor 配置参考 https://docs.lightning.engineering/lightning-network-tools/lnd/quick-tor-setup


## 暴露端口

* 9735  -- P2P 
* 10009 -- rpc

## 创建钱包

```

# lncli state
{
    "state": "NON_EXISTING"
}

# lndinit gen-seed > /root/.lnd/seed.txt

# lndinit -v init-wallet --init-type=rpc  --network=mainnet  --secret-source=file --file.seed=/root/.lnd/seed.txt --file.wallet-password=/root/.lnd/walletpassword.txt --init-rpc.server=localhost:10009 --init-rpc.tls-cert-path=/root/.lnd/tls.cert

# lncli state
{
    "state": "RPC_ACTIVE"
}

```

## 获取信息

```
$ kubectl exec -n default lnd-0 -c lnd -- lncli state
{
    "state":  "LOCKED"
}

$ kubectl exec -n default lnd-0 -c lnd -- bash -c "echo 'pwd' | lncli unlock --stdin"

lnd successfully unlocked!

$ kubectl exec -n default lnd-0 -c lnd -- lncli getinfo
{
    "version":  "0.18.2-beta commit=v0.18.2-beta",
    "commit_hash":  "d22b3937eae91d33cd8c035e8fa894e3793e1636",
    "identity_pubkey":  "03ef1bff239ec9c0317f057bb093f75b7dc98678f237ef3cbcd15b6494a612eaa1",
    "alias":  "03ef1bff239ec9c0317f",
    "color":  "#3399ff",
    "num_pending_channels":  0,
    "num_active_channels":  0,
    "num_inactive_channels":  0,
    "num_peers":  5,
    "block_height":  858605,
    "block_hash":  "00000000000000000002798c625a1bc372616bf2c58b0286572f57e68b58c333",
    "best_header_timestamp":  "1724738827",
    "synced_to_chain":  true,
    "synced_to_graph":  false,
    "testnet":  false,
    "chains":  [
        {
            "chain":  "bitcoin",
            "network":  "mainnet"
        }
    ],
    "uris":  [
        "03ef1bff239ec9c0317f057bb093f75b7dc98678f237ef3cbcd15b6494a612eaa1@ys5iyj7uaxrd5inkzb2pxmgjqpl2e3ii44w64kpij3ngywq4tbmd3lqd.onion:9735"
    ],
...
}

$ kubectl exec -n default lnd-0 -c lnd -- lncli walletbalance
{
    "total_balance":  "0",
    "confirmed_balance":  "0",
    "unconfirmed_balance":  "0",
    "locked_balance":  "0",
    "reserved_balance_anchor_chan":  "0",
    "account_balance":  {
        "default":  {
            "confirmed_balance":  "0",
            "unconfirmed_balance":  "0"
        }
    }
}

$ kubectl exec -n default lnd-0 -c lnd -- lncli channelbalance
{
    "balance":  "0",
    "pending_open_balance":  "0",
    "local_balance":  {
        "sat":  "0",
        "msat":  "0"
    },
    "remote_balance":  {
        "sat":  "0",
        "msat":  "0"
    },
    "unsettled_local_balance":  {
        "sat":  "0",
        "msat":  "0"
    },
    "unsettled_remote_balance":  {
        "sat":  "0",
        "msat":  "0"
    },
    "pending_open_local_balance":  {
        "sat":  "0",
        "msat":  "0"
    },
    "pending_open_remote_balance":  {
        "sat":  "0",
        "msat":  "0"
    }
}

$ kubectl exec -n default lnd-0 -c lnd -- lncli listpeers
{
    "peers":  [
        {
            "pub_key":  "024636018bfae0674b64513c8b5c247130f8273c75a93ca6536240a00d7253c132",
            "address":  "jt33u7sxyteeokxptw2bog365wo7pjujdnvmhqdyyrcw37sieo5uihyd.onion:9735",
            "bytes_sent":  "8798",
            "bytes_recv":  "1136697",
            "sat_sent":  "0",
            "sat_recv":  "0",
            "inbound":  false,
            "ping_time":  "771010",
            "sync_type":  "PASSIVE_SYNC",
            "features":  {
                "0":  {
                    "name":  "data-loss-protect",
                    "is_required":  true,
                    "is_known":  true
                },
                "5":  {
                    "name":  "upfront-shutdown-script",
                    "is_required":  false,
                    "is_known":  true
                },
                "7":  {
                    "name":  "gossip-queries",
                    "is_required":  false,
                    "is_known":  true
                },
                "9":  {
                    "name":  "tlv-onion",
                    "is_required":  false,
                    "is_known":  true
                },
                "12":  {
                    "name":  "static-remote-key",
                    "is_required":  true,
                    "is_known":  true
                },
                "14":  {
                    "name":  "payment-addr",
                    "is_required":  true,
                    "is_known":  true
                },
                "17":  {
                    "name":  "multi-path-payments",
                    "is_required":  false,
                    "is_known":  true
                },
                "23":  {
                    "name":  "anchors-zero-fee-htlc-tx",
                    "is_required":  false,
                    "is_known":  true
                },
                "27":  {
                    "name":  "shutdown-any-segwit",
                    "is_required":  false,
                    "is_known":  true
                },
                "31":  {
                    "name":  "amp",
                    "is_required":  false,
                    "is_known":  true
                },
                "45":  {
                    "name":  "explicit-commitment-type",
                    "is_required":  false,
                    "is_known":  true
                },
                "2023":  {
                    "name":  "script-enforced-lease",
                    "is_required":  false,
                    "is_known":  true
                }
            },
            "errors":  [],
            "flap_count":  3,
            "last_flap_ns":  "1724738676200092500",
            "last_ping_payload":  "00c0c62a14bfb9f27502b0dad32d09e7e71e73010429169a33c3020000000000000000004df65771b68ea1adcb63e76172c3517392a3b2fe11fcb0ab8d5e80e5151b0ee40b6dcd66763d031742faecb9"
        },
    ]
}

$ kubectl exec -n default lnd-0 -c lnd -- lncli listchannels
{
    "channels":  [
        {
            "active":  false,
            "remote_pubkey":  "0309b50815ad6648a731d2d51638b939f9055a6998abc71a59f17094ff93a1ca08",
            "channel_point":  "3fe850d3ead103715b14a08bec3959ebc3a9256284ebe61642131ec7a1f47536:0",
            "chan_id":  "3160469208461017088",
            "capacity":  "50000",
            "local_balance":  "26530",
            "remote_balance":  "20000",
            "commit_fee":  "2810",
            "commit_weight":  "1116",
            "fee_per_kw":  "2500",
            "unsettled_balance":  "0",
            "total_satoshis_sent":  "20000",
            "total_satoshis_received":  "0",
            "num_updates":  "4",
            "pending_htlcs":  [],
            "csv_delay":  144,
            "private":  true,
            "initiator":  true,
            "chan_status_flags":  "ChanStatusDefault",
            "local_chan_reserve_sat":  "500",
            "remote_chan_reserve_sat":  "500",
            "static_remote_key":  false,
            "commitment_type":  "ANCHORS",
            "lifetime":  "10363",
            "uptime":  "0",
            "close_address":  "",
            "push_amount_sat":  "0",
            "thaw_height":  0,
            "local_constraints":  {
                "csv_delay":  144,
                "chan_reserve_sat":  "500",
                "dust_limit_sat":  "354",
                "max_pending_amt_msat":  "49500000",
                "min_htlc_msat":  "1",
                "max_accepted_htlcs":  483
            },
            "remote_constraints":  {
                "csv_delay":  144,
                "chan_reserve_sat":  "500",
                "dust_limit_sat":  "354",
                "max_pending_amt_msat":  "49500000",
                "min_htlc_msat":  "1",
                "max_accepted_htlcs":  483
            },
            "alias_scids":  [],
            "zero_conf":  false,
            "zero_conf_confirmed_scid":  "0",
            "peer_alias":  "0309b50815ad6648a731",
            "peer_scid_alias":  "0",
            "memo":  ""
        }
    ]
}

$ kubectl exec -n default lnd-0 -c lnd -- lncli feereport
{
    "channel_fees": [],
    "day_fee_sum": "0",
    "week_fee_sum": "0",
    "month_fee_sum": "0"
}

$ kubectl exec -n default lnd-0 -c lnd -- lncli getchaninfo 743145615608774656
{
    "channel_id": "743145615608774656",
    "chan_point": "2b91c69a05082d05d7135b41806cc34303837ea10383d1ac3eef77969f98d16e:0",
    "last_update": 1616482074,
    "node1_pub": "021c97a90a411ff2b10dc2a8e32de2f29d2fa49d41bfbb52bd416e460db0747d0d",
    "node2_pub": "032d5a4b5a6a344ca15f6284e3e149f4716a1af782ffbb0194e0dadc077051acf0",
    "capacity": "16777215",
    "node1_policy": {
        "time_lock_delta": 40,
        "min_htlc": "1000",
        "fee_base_msat": "1000",
        "fee_rate_milli_msat": "500",
        "disabled": false,
        "max_htlc_msat": "16609443000",
        "last_update": 1616480497
    },
  "node2_policy": {
        "time_lock_delta": 40,
        "min_htlc": "1000",
        "fee_base_msat": "1000",
        "fee_rate_milli_msat": "1000",
        "disabled": false,
        "max_htlc_msat": "16609443000",
        "last_update": 1616482074
    }
}

$ kubectl exec -n default lnd-0 -c lnd -- xxd -p -c 1000 /root/.lnd/data/chain/bitcoin/mainnet/admin.macaroon
0201036c6e6402f801030a1004a6c6b76397b203c439b0880a4333011201301a160a0761646472657373120472656164120577726974651a130a04696e666f120472656164120577726974651a170a08696e766f69636573120472656164120577726974651a210a086d616361726f6f6e120867656e6572617465120472656164120577726974651a160a076d657373616765120472656164120577726974651a170a086f6666636861696e120472656164120577726974651a160a076f6e636861696e120472656164120577726974651a140a057065657273120472656164120577726974651a180a067369676e6572120867656e6572617465120472656164000006201c492b8bd860534f68b7e465dd787239e84c2e570bfc34bd150f17cb11b7c632

$ kubectl exec -n default lnd-0 -c lnd -- cat /root/.lnd/tls.cert
-----BEGIN CERTIFICATE-----
MIICRDCCAeqgAwIBAgIQcRgOvAHJxLYSQBOyo4lO6DAKBggqhkjOPQQDAjAxMR8w
HQYDVQQKExZsbmQgYXV0b2dlbmVyYXRlZCBjZXJ0MQ4wDAYDVQQDEwVsbmQtMDAe
Fw0yNDA5MDQwOTEyMjVaFw0yNTEwMzAwOTEyMjVaMDExHzAdBgNVBAoTFmxuZCBh
dXRvZ2VuZXJhdGVkIGNlcnQxDjAMBgNVBAMTBWxuZC0wMFkwEwYHKoZIzj0CAQYI
KoZIzj0DAQcDQgAE1N9EoKwhv7aTcguJzRt2hiEdpuunRFoLRLdtM2N/XWZVhPyt
38LzJFVZMY1LbbkHoFJoy8aKnCAC+c4/pjcjOqOB4zCB4DAOBgNVHQ8BAf8EBAMC
AqQwEwYDVR0lBAwwCgYIKwYBBQUHAwEwDwYDVR0TAQH/BAUwAwEB/zAdBgNVHQ4E
FgQUccPzqaeq3E4Ko0Df9iGOsWk6XJQwgYgGA1UdEQSBgDB+ggVsbmQtMIIJbG9j
YWxob3N0gglsbmQtMC5sbmSCCWxuZC0xLmxuZIIJbG5kLTIubG5kggR1bml4ggp1
bml4cGFja2V0ggdidWZjb25uhwR/AAABhxAAAAAAAAAAAAAAAAAAAAABhwQKKgA9
hxD+gAAAAAAAAIRF3P/+LJecMAoGCCqGSM49BAMCA0gAMEUCIBCT/B3OaHdDmf8/
EwnXYhiffX/v1XSk7tiWMcOBSBxlAiEAs0v/e0WGmsHlw/4Y3ueYhRljld+k+RR7
lAAmrJfnDbw=
-----END CERTIFICATE-----

```