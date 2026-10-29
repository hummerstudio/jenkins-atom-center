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

索引由 `index.json.sig` 签名。**官方中心的公钥内置在插件里**（`AtomOfficialKeys`），管理员不需要填写任何东西：
插件只对这个中心 URL（`AtomNames.DEFAULT_CENTER_URL`）使用内置公钥，指向别处的同一份索引不会被自动信任。

| keyId | 用途 |
|---|---|
| `atom-center-2026` | 最初的示例原子；私钥已不可得，仍保留以便老镜像继续验签 |
| `atom-center-2026b` | 当前签名密钥（`keys/atom-center-2026b.pub.b64`） |

**自建/私有中心**才需要在 `Manage Jenkins -> Atom Center -> 设置 -> 受信任公钥` 里填 `keyId=base64`，一行一把；
这是私服的信任根，官方中心用不到。

换钥匙意味着新版本插件内置新公钥：升级前实例继续用手里那把内置公钥验旧索引（不刷新、不报错），
升级后自动接受新签名。私服换钥匙则要自己改配置。
