# jenkins-atom-center

The default atom center for the `jenkins-atom-runner` Jenkins plugin.

Clients read `index.json` from `main`:

```
https://raw.githubusercontent.com/hummerstudio/jenkins-atom-center/main/index.json
```

Publish an atom with `tools/publish-atom.sh` from `jenkins-atom-plugin`; the script appends the version to
`index.json`, writes the package zip, and (when a key is configured) signs the index with `index.json.sig`.

## 已发布（`publisher = hummerstudio`）

| atom | 版本 | 说明 |
|---|---|---|
| `rebuild` | 1.0.0 | 构建页 Rebuild 入口，0 行代码（`ui.json`） |
| `build-name-setter` | 1.0.0 | 模板 + 日志正则改名、写描述（`mutations.json`） |
| `http-request` | 1.0.0 | 调接口，出参 status/body/headers |
| `ant` / `maven` / `gradle` | 1.0.0 | 跑构建工具，退出码即结果 |
| `mail` | 1.0.0 | SMTP 发信（mailer + email-ext 常用部分） |

每个原子一个仓库：`hummerstudio/jenkins-atom-<atom>`。

## 签名密钥

索引由 `index.json.sig` 签名，公钥在 `keys/`：

- `atom-center-2026` — 第一把钥匙，仅用于最初的示例原子；**私钥已不可得**（只保留公钥）。
- `atom-center-2026b` — 当前签名密钥（`keys/atom-center-2026b.pub.b64` 即 Jenkins 全局配置里要填的值）。

换钥匙意味着客户端要显式信任新公钥：`Manage Jenkins -> Atom Center -> 设置 -> 可信密钥` 里加一行
`atom-center-2026b=<b64>`。索引重签后，只信任旧钥匙的实例会拒绝刷新（并继续使用本地已验签的旧副本），
这是设计上的行为，不是故障。
