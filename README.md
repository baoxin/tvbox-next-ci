# tvbox-next-ci

[TVBox-Next](https://github.com/baoxin/TVBox-Next)（私有仓库）的免费构建通道：本仓库定时巡检私有仓库的新 tag，检出源码构建 APK 并回发到私有仓库的 release。构建消耗公共仓库的免费 Actions 额度，私有仓库零用量。

## 工作方式

- 每 30 分钟巡检一次：发现「还没有 release 的 `v*` tag」就构建，APK 回发到该 tag 的 release；
- 手动运行：填 tag 强制重建该 tag（release 资产同名覆盖）；不填则构建默认分支、仅产出 artifact（公共仓库 artifact 任何人可下载，注意）；
- GitHub 会在仓库 60 天无活动后自动停用 schedule，长时间不发包时在 Actions 里手动跑一次即可保活。

## 所需 secrets

| Secret | 说明 |
| --- | --- |
| `PRIVATE_REPO_TOKEN` | baoxin 账号的 fine-grained PAT，仅授权 `baoxin/TVBox-Next`，权限 Contents: Read and write |
