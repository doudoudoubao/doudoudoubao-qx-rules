# doudoudoubao-qx-rules

Quantumult X 分流规则。

## Meta 全家桶（Meta.list）

覆盖 Meta Platforms 旗下全部 App：Facebook / Messenger / Instagram / WhatsApp /
Threads / Meta Quest(Oculus) / Meta AI / Llama / Workplace / Mapillary / Wit.ai，
共 54 条规则（含 Meta 自有 ASN 兜底）。

### 一键加入

在 iOS 上点开下面的链接，QX 会弹窗询问是否添加资源，确认即可：

```
quantumult-x:///add-resource?remote-resource=%7B%22filter_remote%22%3A%5B%22https%3A%2F%2Fraw.githubusercontent.com%2Fdoudoudoubao%2Fdoudoudoubao-qx-rules%2Fmain%2FMeta.list%2C%20tag%3DMeta%2C%20force-policy%3Dproxy%2C%20update-interval%3D86400%2C%20opt-parser%3Dfalse%2C%20enabled%3Dtrue%22%5D%7D
```

raw.githubusercontent.com 更新超时的话，用 jsDelivr 镜像版：

```
quantumult-x:///add-resource?remote-resource=%7B%22filter_remote%22%3A%5B%22https%3A%2F%2Fcdn.jsdelivr.net%2Fgh%2Fdoudoudoubao%2Fdoudoudoubao-qx-rules%40main%2FMeta.list%2C%20tag%3DMeta%2C%20force-policy%3Dproxy%2C%20update-interval%3D86400%2C%20opt-parser%3Dfalse%2C%20enabled%3Dtrue%22%5D%7D
```

加完后在 QX 的 `[filter_remote]` 里能看到 `tag=Meta` 的条目。
想换策略组，把那一行的 `force-policy=proxy` 改成 `force-policy=你的策略组名`。

### 不用托管，直接粘贴

把 [`Meta-filter_local.txt`](Meta-filter_local.txt) 整段粘进配置文件的
`[filter_local]` 段，策略已写成内置 `proxy`，放在 `geoip, cn, direct` 和 `final` 之前。

### 只要一条

```
[filter_local]
ip-asn, 32934, proxy
```

按 Meta 自有 ASN 匹配，一行兜住绝大部分 Meta 流量。

## 文件说明

| 文件 | 用途 |
|---|---|
| `Meta.list` | `[filter_remote]` 远程资源，策略靠 `force-policy=` 覆盖 |
| `Meta-filter_local.txt` | `[filter_local]` 直贴版，策略已写成 `proxy` |

## 注意

1. **顺序优先**：QX 从上往下匹配，Meta 规则必须在 `geoip, cn, direct` 和 `final` 之前。
2. `[filter_remote]` 优先级低于 `[filter_local]`，两边冲突时 local 赢。
3. `HOST-KEYWORD` 段是给 `scontent-xxx.xx.fbcdn.net` 这类各地区节点兜底的，
   副作用是会误伤含 facebook/instagram/oculus 字样的第三方域名（都走代理，无害）。
   介意就删掉那 5 行。
4. `IP-ASN` 需要 QX 1.0.20+；不生效就把 `Meta.list` 末尾注释掉的 `IP-CIDR` 段放开。
5. 已排除非 Meta 资产：giphy.com（2023 年售予 Shutterstock）、kustomer.com（已出售）、
   ray-ban.com（属 EssilorLuxottica）。
