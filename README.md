# doudoudoubao-qx-rules

Quantumult X 分流规则。

## Meta 全家桶（Meta.list）

覆盖 Meta Platforms 旗下全部 App：Facebook / Messenger / Instagram / WhatsApp /
Threads / Meta Quest(Oculus) / Meta AI / Llama / Workplace / Mapillary / Wit.ai，
共 54 条规则（含 Meta 自有 ASN 兜底）。

---

## 方式一：一键加入（Universal Link，推荐）

在 **iOS 上用 Safari 打开** 本页面，然后直接点这个链接，QX 会弹窗确认：

👉 [**一键加入 Meta 规则**](https://quantumult.app/x/open-app/add-resource?remote-resource=%7B%22filter_remote%22%3A%5B%22https%3A%2F%2Fraw.githubusercontent.com%2Fdoudoudoubao%2Fdoudoudoubao-qx-rules%2Fmain%2FMeta.list%2C%20tag%3DMeta%2C%20force-policy%3Dproxy%2C%20enabled%3Dtrue%22%5D%7D)

国内 raw.githubusercontent 拉取超时的话用 jsDelivr 镜像：

👉 [**一键加入（jsDelivr 镜像）**](https://quantumult.app/x/open-app/add-resource?remote-resource=%7B%22filter_remote%22%3A%5B%22https%3A%2F%2Fcdn.jsdelivr.net%2Fgh%2Fdoudoudoubao%2Fdoudoudoubao-qx-rules%40main%2FMeta.list%2C%20tag%3DMeta%2C%20force-policy%3Dproxy%2C%20enabled%3Dtrue%22%5D%7D)

> Universal Link 需要 QX 1.0.30+。若点击后跳到 Safari 网页而不是 QX，
> 说明系统还没缓存 QX 的 apple-app-site-association（装机后约一周刷新一次），
> 改用下面的方式二或方式三。

## 方式二：URL Scheme

把下面整行复制，粘贴到 **Safari 地址栏**回车（注意：微信、备忘录等 App 里不可点）：

```
quantumult-x:///add-resource?remote-resource=%7B%22filter_remote%22%3A%5B%22https%3A%2F%2Fraw.githubusercontent.com%2Fdoudoudoubao%2Fdoudoudoubao-qx-rules%2Fmain%2FMeta.list%2C%20tag%3DMeta%2C%20force-policy%3Dproxy%2C%20enabled%3Dtrue%22%5D%7D
```

jsDelivr 镜像版：

```
quantumult-x:///add-resource?remote-resource=%7B%22filter_remote%22%3A%5B%22https%3A%2F%2Fcdn.jsdelivr.net%2Fgh%2Fdoudoudoubao%2Fdoudoudoubao-qx-rules%40main%2FMeta.list%2C%20tag%3DMeta%2C%20force-policy%3Dproxy%2C%20enabled%3Dtrue%22%5D%7D
```

## 方式三：手动添加（最稳，一定成功）

QX → 底部 **设置** → **配置文件** → **编辑**，找到 `[filter_remote]` 段，加一行：

```
https://raw.githubusercontent.com/doudoudoubao/doudoudoubao-qx-rules/main/Meta.list, tag=Meta, force-policy=proxy, enabled=true
```

保存后回首页下拉刷新即可。

## 方式四：完全不用托管，直接粘贴规则

把 [`Meta-filter_local.txt`](Meta-filter_local.txt) 整段粘进 `[filter_local]` 段，
策略已写成内置 `proxy`，放在 `geoip, cn, direct` 和 `final` 之前。

## 方式五：只要一条

```
[filter_local]
ip-asn, 32934, proxy
```

按 Meta 自有 ASN 匹配，一行兜住绝大部分 Meta 流量。

---

## 文件说明

| 文件 | 用途 |
|---|---|
| `Meta.list` | `[filter_remote]` 远程资源，策略靠 `force-policy=` 覆盖 |
| `Meta-filter_local.txt` | `[filter_local]` 直贴版，策略已写成 `proxy` |

## 注意

1. **顺序优先**：QX 从上往下匹配，Meta 规则必须在 `geoip, cn, direct` 和 `final` 之前。
2. `[filter_remote]` 优先级低于 `[filter_local]`，两边冲突时 local 赢。
3. `force-policy=proxy` 里的 `proxy` 是 QX 内置策略，想走自己的策略组就改成组名。
4. `filter_remote` 的合法参数只有 `tag` / `force-policy` / `enabled` /
   `inserted-resource` / `require-devices`（`update-interval`、`opt-parser`
   属于 `[server_remote]`，别往这儿写）。资源自动更新间隔在 QX 全局设置里调。
5. `HOST-KEYWORD` 段是给 `scontent-xxx.xx.fbcdn.net` 这类各地区节点兜底的，
   副作用是会误伤含 facebook/instagram/oculus 字样的第三方域名（都走代理，无害）。
6. `IP-ASN` 需要 QX 1.0.20+；不生效就把 `Meta.list` 末尾注释掉的 `IP-CIDR` 段放开。
7. 已排除非 Meta 资产：giphy.com（2023 年售予 Shutterstock）、kustomer.com（已出售）、
   ray-ban.com（属 EssilorLuxottica）。
