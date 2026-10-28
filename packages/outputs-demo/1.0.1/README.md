# Outputs demo

演示原子如何把结果交回 Jenkins：

- **环境变量**：`branch`、`artifactUrl` 注入为 `ATOM_BRANCH` / `ATOM_ARTIFACTURL`，后续步骤可直接用；
- **敏感值**：`token` 标记 `isSensitive`，页面显示 `********`；
- **报告**：`coverage` 是归档 HTML，构建页内嵌预览；`dashboard` 是纯链接；
- **制品**：`package` 归档 `report.json`。

## 用法

```groovy
runAtom(atom: 'outputs-demo', version: '1.0.1')
```
