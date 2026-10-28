# SDK 能力演示

覆盖 `com.jenkinschina:jenkins-atom-sdk` 的主要接口：

| 能力 | 入口 |
| --- | --- |
| 读取输入 | `params.get("msg")` |
| 写输出 | `result.data.put(...)` |
| 运行脚本 | `Shell.sh("echo hi")` |
| 失败语义 | `result.status = "failure"` + `errorCode` |

## 输入

- `mode`：`string` / `artifact` / `report` / `failure` / `logs` 等十种模式；
- `msg`、`count`、`dryRun`、`tags`、`reportDir`、`image_name`、`jsonText`。

## 运行

```groovy
runAtom(atom: 'sdk-demo', version: '1.0.1', inputs: [mode: 'logs'])
```
