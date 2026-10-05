# QuanX shared routing rules

从合并后的 Mac / iPhone 配置中提取的 164 条域名分流规则。仅包含域名、匹配方式和策略组名称；不包含节点订阅、密码、token、证书或 DNS 配置。

## 订阅

Raw 地址：

https://raw.githubusercontent.com/Trimmy7/quanx-rules/main/routing.list

在 QuanX 配置的 `[filter_remote]` 开头添加：

```ini
https://raw.githubusercontent.com/Trimmy7/quanx-rules/main/routing.list, tag=Trimmy-Shared, update-interval=3600, opt-parser=false, inserted-resource=true, enabled=true
```

不要设置 `force-policy`，每条规则使用文件里指定的策略组。订阅加载成功后，移除设备 `[filter_local]` 中对应的域名规则，避免本地规则覆盖 GitHub 更新；局域网、IP、GEOIP 和 final 兜底仍留在设备配置里。

## 修改与同步

在 GitHub 修改 `routing.list`，设备刷新资源后生效。自动更新间隔为 1 小时，也可手动更新。保留规则顺序：更具体的域名规则和已有优先级可能影响匹配。

在 QuanX 中新增的本地规则不会自动推送到 GitHub。需要共用的新规则应修改本仓库。

## 策略组

手机和电脑需要具有下列同名策略组：

AI通用, Bybit, Claude, Copilot, Fast Sfct, GitHub, Google, Meta, OpenAI, Perplexity, SpaceX, Sufficient, Wise, porn, xAI, 全球加速, 台湾节点, 狮城节点

Google 搜索、Gmail、Drive、YouTube、Gemini、NotebookLM、登录、API 和静态资源统一使用 `Google` 组。关联的 iCloud 配置将 Google 固定到 `US - Los Angeles - Quanx`，原 Gemini 组作为指向 Google 的兼容入口。Google、Gemini、Google Voice 的远程规则订阅均使用 `force-policy=Google`。仅订阅本仓库的设备需要自行完成策略组设置。
